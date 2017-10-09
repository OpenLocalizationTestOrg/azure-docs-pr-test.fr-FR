---
title: "aaaBack d’un tooAzure du serveur Exchange sauvegarde avec System Center 2012 R2 DPM | Documents Microsoft"
description: "Découvrez comment tooback d’un tooAzure du serveur Exchange de sauvegarde à l’aide de System Center 2012 R2 DPM"
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="e2078-103">Sauvegarder un tooAzure du serveur Exchange sauvegarde avec System Center 2012 R2 DPM</span><span class="sxs-lookup"><span data-stu-id="e2078-103">Back up an Exchange server tooAzure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="e2078-104">Cet article décrit comment tooconfigure un tooback du serveur System Center 2012 R2 Data Protection Manager (DPM) d’un serveur Microsoft Exchange trop Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="e2078-104">This article describes how tooconfigure a System Center 2012 R2 Data Protection Manager (DPM) server tooback up a Microsoft Exchange server too Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="e2078-105">Mises à jour</span><span class="sxs-lookup"><span data-stu-id="e2078-105">Updates</span></span>
<span data-ttu-id="e2078-106">serveur DPM hello toosuccessfully register avec Azure Backup, vous devez installer hello dernier correctif cumulatif pour System Center 2012 R2 DPM et hello version la plus récente de hello Azure Backup Agent.</span><span class="sxs-lookup"><span data-stu-id="e2078-106">toosuccessfully register hello DPM server with Azure Backup, you must install hello latest update rollup for System Center 2012 R2 DPM and hello latest version of hello Azure Backup Agent.</span></span> <span data-ttu-id="e2078-107">Obtenir hello dernier correctif cumulatif de mise à jour à partir de hello [catalogue Microsoft](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="e2078-107">Get hello latest update rollup from hello [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="e2078-108">Pour obtenir des exemples hello dans cet article, la version 2.0.8719.0 de hello Azure Backup Agent est installée et correctif cumulatif 6 est installé sur System Center 2012 R2 DPM.</span><span class="sxs-lookup"><span data-stu-id="e2078-108">For hello examples in this article, version 2.0.8719.0 of hello Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="e2078-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e2078-109">Prerequisites</span></span>
<span data-ttu-id="e2078-110">Avant de continuer, assurez-vous que tous les hello [conditions préalables](backup-azure-dpm-introduction.md#prerequisites) pour l’utilisation de Microsoft Azure Backup tooprotect les charges de travail ont été remplies.</span><span class="sxs-lookup"><span data-stu-id="e2078-110">Before you continue, make sure that all hello [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup tooprotect workloads have been met.</span></span> <span data-ttu-id="e2078-111">Ces conditions préalables hello suivants :</span><span class="sxs-lookup"><span data-stu-id="e2078-111">These prerequisites include hello following:</span></span>

* <span data-ttu-id="e2078-112">Un coffre de sauvegarde sur hello site Azure a été créé.</span><span class="sxs-lookup"><span data-stu-id="e2078-112">A backup vault on hello Azure site has been created.</span></span>
* <span data-ttu-id="e2078-113">Informations d’identification de l’agent et le coffre ont été téléchargés toohello le serveur DPM.</span><span class="sxs-lookup"><span data-stu-id="e2078-113">Agent and vault credentials have been downloaded toohello DPM server.</span></span>
* <span data-ttu-id="e2078-114">agent de Hello est installé sur le serveur DPM hello.</span><span class="sxs-lookup"><span data-stu-id="e2078-114">hello agent is installed on hello DPM server.</span></span>
* <span data-ttu-id="e2078-115">informations d’identification de coffre Hello ont été serveur DPM de hello tooregister utilisé.</span><span class="sxs-lookup"><span data-stu-id="e2078-115">hello vault credentials were used tooregister hello DPM server.</span></span>
* <span data-ttu-id="e2078-116">Si vous protégez Exchange 2016, mettez à niveau tooDPM 2012 R2 UR9 ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="e2078-116">If you are protecting Exchange 2016, please upgrade tooDPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="e2078-117">Agent de protection DPM</span><span class="sxs-lookup"><span data-stu-id="e2078-117">DPM protection agent</span></span>
<span data-ttu-id="e2078-118">agent de protection DPM tooinstall hello sur le serveur Exchange de hello, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e2078-118">tooinstall hello DPM protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="e2078-119">Assurez-vous que les pare-feux hello est correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="e2078-119">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="e2078-120">Consultez [configurer des exceptions de pare-feu pour l’agent de hello](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2078-120">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="e2078-121">Installer l’agent de hello sur le serveur Exchange de hello en cliquant sur **Gestion > Agents > installer** dans la Console Administrateur DPM.</span><span class="sxs-lookup"><span data-stu-id="e2078-121">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="e2078-122">Consultez [agent de protection DPM installation hello](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) pour obtenir des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="e2078-122">See [Install hello DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="e2078-123">Créer un groupe de protection pour Exchange server de hello</span><span class="sxs-lookup"><span data-stu-id="e2078-123">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="e2078-124">Bonjour la Console Administrateur DPM, cliquez sur **Protection**, puis cliquez sur **nouveau** sur Bonjour outil ruban tooopen Bonjour **créer un nouveau groupe de Protection** Assistant.</span><span class="sxs-lookup"><span data-stu-id="e2078-124">In hello DPM Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="e2078-125">Sur hello **Bienvenue** écran de hello, cliquez sur Assistant **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-125">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="e2078-126">Sur hello **sélectionner le type de groupe de protection** , sélectionnez **serveurs** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-126">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="e2078-127">Base de données Sélectionnez hello Exchange server que vous souhaitez tooprotect, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-127">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e2078-128">Si vous protégez Exchange 2013, vérifiez hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="e2078-128">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="e2078-129">Bonjour l’exemple suivant, la base de données hello Exchange 2010 est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="e2078-129">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Sélectionner les membres du groupe](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="e2078-131">Sélectionnez la méthode de protection des données hello.</span><span class="sxs-lookup"><span data-stu-id="e2078-131">Select hello data protection method.</span></span>

    <span data-ttu-id="e2078-132">Nom de groupe de protection hello et sélectionnez les deux hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="e2078-132">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="e2078-133">Je souhaite une protection à court terme à l’aide de Disque.</span><span class="sxs-lookup"><span data-stu-id="e2078-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="e2078-134">Je voudrais une protection en ligne.</span><span class="sxs-lookup"><span data-stu-id="e2078-134">I want online protection.</span></span>
6. <span data-ttu-id="e2078-135">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-135">Click **Next**.</span></span>
7. <span data-ttu-id="e2078-136">Sélectionnez hello **l’intégrité des données toocheck exécuter Eseutil** option si vous souhaitez que l’intégrité de hello toocheck des bases de données Exchange Server hello.</span><span class="sxs-lookup"><span data-stu-id="e2078-136">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="e2078-137">Une fois que vous sélectionnez cette option, la vérification de cohérence de sauvegarde sur est exécutée hello DPM tooavoid hello d’e/s le trafic du serveur qui est généré en exécutant hello **eseutil** commande sur le serveur Exchange de hello.</span><span class="sxs-lookup"><span data-stu-id="e2078-137">After you select this option, backup consistency checking will be run on hello DPM server tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e2078-138">toouse cette option, vous devez copier hello Ese.dll et le répertoire C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin toohello des fichiers Eseutil.exe sur le serveur DPM hello.</span><span class="sxs-lookup"><span data-stu-id="e2078-138">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on hello DPM server.</span></span> <span data-ttu-id="e2078-139">Dans le cas contraire, hello l’erreur suivante est déclenchée :</span><span class="sxs-lookup"><span data-stu-id="e2078-139">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="e2078-140">![erreur eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="e2078-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="e2078-141">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-141">Click **Next**.</span></span>
9. <span data-ttu-id="e2078-142">Base de données Sélectionnez hello pour **sauvegarde de copie**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-142">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e2078-143">Si vous ne sélectionnez pas « Sauvegarde complète » pour au moins une copie DAG d’une base de données, les journaux ne seront pas tronqués.</span><span class="sxs-lookup"><span data-stu-id="e2078-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="e2078-144">Configurer les objectifs de hello pour **sauvegarde à court terme**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-144">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="e2078-145">Passez en revue l’espace disque disponible hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-145">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="e2078-146">Sélectionnez heure hello à quels hello DPM server sera créé, la réplication initiale hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-146">Select hello time at which hello DPM server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="e2078-147">Sélectionnez les options de vérification de cohérence hello, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-147">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="e2078-148">Choisissez hello la base de données que vous souhaitez tooback les tooAzure, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-148">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="e2078-149">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e2078-149">For example:</span></span>

    ![Spécifier les données de protection en ligne](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="e2078-151">Définir la planification de hello pour **Azure Backup**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-151">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="e2078-152">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="e2078-152">For example:</span></span>

    ![Spécifier la planification de sauvegarde en ligne](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="e2078-154">Notez que les points de récupération en ligne sont basés sur des points de récupération complète express.</span><span class="sxs-lookup"><span data-stu-id="e2078-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="e2078-155">Par conséquent, vous devez planifier un point de récupération hello après hello est spécifié pour hello express point de récupération complète.</span><span class="sxs-lookup"><span data-stu-id="e2078-155">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="e2078-156">Configurer la stratégie de rétention hello pour **Azure Backup**, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-156">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="e2078-157">Choisissez une option de réplication en ligne, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e2078-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="e2078-158">Si vous avez une base de données volumineux, il peut prendre beaucoup de temps pour toobe sauvegarde initiale hello créée via le réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="e2078-158">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="e2078-159">tooavoid ce problème, vous pouvez créer une sauvegarde hors connexion.</span><span class="sxs-lookup"><span data-stu-id="e2078-159">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Spécifier la stratégie de rétention en ligne](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="e2078-161">Confirmez les paramètres de hello, puis cliquez sur **créer un groupe**.</span><span class="sxs-lookup"><span data-stu-id="e2078-161">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="e2078-162">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="e2078-162">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="e2078-163">Récupérer la base de données Exchange hello</span><span class="sxs-lookup"><span data-stu-id="e2078-163">Recover hello Exchange database</span></span>
1. <span data-ttu-id="e2078-164">toorecover une base de données Exchange, cliquez sur **récupération** Bonjour la Console Administrateur DPM.</span><span class="sxs-lookup"><span data-stu-id="e2078-164">toorecover an Exchange database, click **Recovery** in hello DPM Administrator Console.</span></span>
2. <span data-ttu-id="e2078-165">Localisez la base de données Exchange hello que vous souhaitez toorecover.</span><span class="sxs-lookup"><span data-stu-id="e2078-165">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="e2078-166">Sélectionnez un point de récupération en ligne à partir de hello *temps de récupération* liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="e2078-166">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="e2078-167">Cliquez sur **récupérer** toostart hello **Assistant récupération**.</span><span class="sxs-lookup"><span data-stu-id="e2078-167">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="e2078-168">Pour les points de récupération en ligne, il existe cinq types de récupération :</span><span class="sxs-lookup"><span data-stu-id="e2078-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="e2078-169">**Récupérer l’emplacement du serveur Exchange toooriginal :** les données de salutation sera récupérée toohello d’origine Exchange server.</span><span class="sxs-lookup"><span data-stu-id="e2078-169">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="e2078-170">**Récupérer la base de données tooanother sur un serveur Exchange :** les données de salutation seront récupérés tooanother de base de données sur un autre serveur Exchange.</span><span class="sxs-lookup"><span data-stu-id="e2078-170">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="e2078-171">**Récupérer tooa de base de données de récupération :** les données de salutation seront récupéré tooan de base de données de récupération Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="e2078-171">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="e2078-172">**Copier le dossier réseau tooa :** les données de salutation sera récupérée tooa dossier du réseau.</span><span class="sxs-lookup"><span data-stu-id="e2078-172">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="e2078-173">**Copiez tootape :** si vous avez une bibliothèque de bandes ou un lecteur de bande autonome hello attaché et configuré sur le serveur DPM, point de récupération hello seront copiés les bandes libres tooa.</span><span class="sxs-lookup"><span data-stu-id="e2078-173">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on hello DPM server, hello recovery point will be copied tooa free tape.</span></span>

    ![Choisir la réplication en ligne](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="e2078-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e2078-175">Next steps</span></span>
* [<span data-ttu-id="e2078-176">Azure Backup - Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="e2078-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
