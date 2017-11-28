---
title: Sauvegarder un serveur Exchange dans Azure Backup avec System Center 2012 R2 DPM | Microsoft Docs
description: "Apprenez à sauvegarder un serveur Exchange dans Azure Backup à l’aide de System Center 2012 R2 DPM"
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
ms.openlocfilehash: 2a0e416440e55cfde70cbd20d40c99fb29b4229c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="35597-103">Sauvegarder un serveur Exchange dans Azure Backup avec System Center 2012 R2 DPM</span><span class="sxs-lookup"><span data-stu-id="35597-103">Back up an Exchange server to Azure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="35597-104">Cet article explique comment configurer un serveur System Center 2012 R2 Data Protection Manager (DPM) pour sauvegarder un serveur Microsoft Exchange dans Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="35597-104">This article describes how to configure a System Center 2012 R2 Data Protection Manager (DPM) server to back up a Microsoft Exchange server to  Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="35597-105">Mises à jour</span><span class="sxs-lookup"><span data-stu-id="35597-105">Updates</span></span>
<span data-ttu-id="35597-106">Pour enregistrer correctement le serveur DPM sur Azure Backup, vous devez installer le dernier correctif cumulatif pour System Center 2012 R2 DPM ainsi que la dernière version de l’agent Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="35597-106">To successfully register the DPM server with Azure Backup, you must install the latest update rollup for System Center 2012 R2 DPM and the latest version of the Azure Backup Agent.</span></span> <span data-ttu-id="35597-107">Pour obtenir le dernier correctif cumulatif, consultez le [catalogue Microsoft](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="35597-107">Get the latest update rollup from the [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="35597-108">Pour les exemples de cet article, nous avons utilisé la version 2.0.8719.0 de l’agent Azure Backup et installé le correctif cumulatif 6 sur System Center 2012 R2 DPM.</span><span class="sxs-lookup"><span data-stu-id="35597-108">For the examples in this article, version 2.0.8719.0 of the Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="35597-109">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="35597-109">Prerequisites</span></span>
<span data-ttu-id="35597-110">Avant de continuer, vérifiez que toutes les [conditions préalables](backup-azure-dpm-introduction.md#prerequisites) à l’utilisation de Microsoft Azure Backup pour protéger les charges de travail ont bien été remplies.</span><span class="sxs-lookup"><span data-stu-id="35597-110">Before you continue, make sure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="35597-111">Vous devez au préalable :</span><span class="sxs-lookup"><span data-stu-id="35597-111">These prerequisites include the following:</span></span>

* <span data-ttu-id="35597-112">Créer un coffre de sauvegarde sur le site Azure.</span><span class="sxs-lookup"><span data-stu-id="35597-112">A backup vault on the Azure site has been created.</span></span>
* <span data-ttu-id="35597-113">Télécharger les informations d’identification de l’agent et du coffre sur le serveur DPM.</span><span class="sxs-lookup"><span data-stu-id="35597-113">Agent and vault credentials have been downloaded to the DPM server.</span></span>
* <span data-ttu-id="35597-114">Installer l’agent sur le serveur DPM.</span><span class="sxs-lookup"><span data-stu-id="35597-114">The agent is installed on the DPM server.</span></span>
* <span data-ttu-id="35597-115">Utiliser les informations d’identification pour enregistrer le serveur DPM.</span><span class="sxs-lookup"><span data-stu-id="35597-115">The vault credentials were used to register the DPM server.</span></span>
* <span data-ttu-id="35597-116">Si vous protégez Exchange 2016, mettez à niveau vers DPM 2012 R2 UR9 ou une version ultérieure</span><span class="sxs-lookup"><span data-stu-id="35597-116">If you are protecting Exchange 2016, please upgrade to DPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="35597-117">Agent de protection DPM</span><span class="sxs-lookup"><span data-stu-id="35597-117">DPM protection agent</span></span>
<span data-ttu-id="35597-118">Pour installer l’agent de protection DPM sur le serveur Exchange, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="35597-118">To install the DPM protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="35597-119">Assurez-vous que les pare-feux sont correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="35597-119">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="35597-120">Consultez la page [Configuration d’exceptions de pare-feu pour l’agent](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="35597-120">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="35597-121">Installez l’agent sur le serveur Exchange en cliquant sur **Gestion > Agents > Installer** dans la Console Administrateur DPM.</span><span class="sxs-lookup"><span data-stu-id="35597-121">Install the agent on the Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="35597-122">Pour obtenir des instructions détaillées, consultez la page [Installation de l’agent de protection DPM](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) .</span><span class="sxs-lookup"><span data-stu-id="35597-122">See [Install the DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="35597-123">Créer un groupe de protection pour le serveur Exchange</span><span class="sxs-lookup"><span data-stu-id="35597-123">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="35597-124">Dans la Console Administrateur DPM, cliquez sur **Protection**, puis cliquez sur **Nouveau** dans la barre d’outils pour ouvrir l’assistant **Créer un nouveau groupe de Protection**.</span><span class="sxs-lookup"><span data-stu-id="35597-124">In the DPM Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="35597-125">Dans l’écran d’**accueil** de l’assistant, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-125">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="35597-126">Dans l’écran **Sélectionner le type de groupe de protection**, sélectionnez **Serveurs**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-126">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="35597-127">Sélectionnez la base de données du serveur Exchange que vous souhaitez protéger, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-127">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="35597-128">Si vous protégez Exchange 2013, vérifiez les [Conditions préalables pour Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="35597-128">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="35597-129">Dans l’exemple suivant, la base de données Exchange 2010 est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="35597-129">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Sélectionner les membres du groupe](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="35597-131">Sélectionnez la méthode de protection des données.</span><span class="sxs-lookup"><span data-stu-id="35597-131">Select the data protection method.</span></span>

    <span data-ttu-id="35597-132">Attribuez un nom au groupe de protection, puis sélectionnez les deux options suivantes :</span><span class="sxs-lookup"><span data-stu-id="35597-132">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="35597-133">Je souhaite une protection à court terme à l’aide de Disque.</span><span class="sxs-lookup"><span data-stu-id="35597-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="35597-134">Je voudrais une protection en ligne.</span><span class="sxs-lookup"><span data-stu-id="35597-134">I want online protection.</span></span>
6. <span data-ttu-id="35597-135">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-135">Click **Next**.</span></span>
7. <span data-ttu-id="35597-136">Sélectionnez l’option **Exécuter Eseutil pour vérifier l’intégrité des données** si vous souhaitez vérifier l’intégrité des bases de données Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="35597-136">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="35597-137">Après avoir sélectionné cette option, une vérification de la cohérence de sauvegarde s’exécutera sur le serveur DPM afin d’éviter le trafic d’E/S généré lors de l’exécution de la commande **eseutil** sur le serveur Exchange.</span><span class="sxs-lookup"><span data-stu-id="35597-137">After you select this option, backup consistency checking will be run on the DPM server to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="35597-138">Pour utiliser cette option, vous devez copier les fichiers Ese.dll et Eseutil.exe dans le répertoire C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin sur le serveur DPM.</span><span class="sxs-lookup"><span data-stu-id="35597-138">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on the DPM server.</span></span> <span data-ttu-id="35597-139">Dans le cas contraire, l’erreur suivante est déclenchée : </span><span class="sxs-lookup"><span data-stu-id="35597-139">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="35597-140">![erreur eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="35597-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="35597-141">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-141">Click **Next**.</span></span>
9. <span data-ttu-id="35597-142">Sélectionnez la base de données pour **Sauvegarde de copie**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-142">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="35597-143">Si vous ne sélectionnez pas « Sauvegarde complète » pour au moins une copie DAG d’une base de données, les journaux ne seront pas tronqués.</span><span class="sxs-lookup"><span data-stu-id="35597-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="35597-144">Configurez les objectifs de **Sauvegarde à court terme**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-144">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="35597-145">Vérifiez l’espace disque disponible, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-145">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="35597-146">Sélectionnez l’heure à laquelle le serveur DPM devra créer la réplication initiale, puis cliquez **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-146">Select the time at which the DPM server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="35597-147">Sélectionnez les options de vérification de cohérence, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-147">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="35597-148">Choisissez la base de données que vous souhaitez sauvegarder sur Azure, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-148">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="35597-149">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="35597-149">For example:</span></span>

    ![Spécifier les données de protection en ligne](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="35597-151">Définissez la planification pour **Azure Backup**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-151">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="35597-152">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="35597-152">For example:</span></span>

    ![Spécifier la planification de sauvegarde en ligne](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="35597-154">Notez que les points de récupération en ligne sont basés sur des points de récupération complète express.</span><span class="sxs-lookup"><span data-stu-id="35597-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="35597-155">Par conséquent, vous devez planifier le point de récupération en ligne après l’heure spécifiée pour le point de récupération complète express.</span><span class="sxs-lookup"><span data-stu-id="35597-155">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="35597-156">Configurer la stratégie de rétention pour **Azure Backup**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-156">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="35597-157">Choisissez une option de réplication en ligne, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="35597-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="35597-158">Si vous disposez d’une base de données volumineuse, la création de la sauvegarde initiale sur le réseau peut prendre un long moment.</span><span class="sxs-lookup"><span data-stu-id="35597-158">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="35597-159">Pour éviter ce problème, vous pouvez créer une sauvegarde hors connexion.</span><span class="sxs-lookup"><span data-stu-id="35597-159">To avoid this issue, you can create an offline backup.</span></span>  

    ![Spécifier la stratégie de rétention en ligne](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="35597-161">Confirmez les paramètres, puis cliquez sur **Créer un groupe**.</span><span class="sxs-lookup"><span data-stu-id="35597-161">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="35597-162">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="35597-162">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="35597-163">Récupérer la base de données Exchange</span><span class="sxs-lookup"><span data-stu-id="35597-163">Recover the Exchange database</span></span>
1. <span data-ttu-id="35597-164">Pour récupérer une base de données Exchange, cliquez sur **Récupération** dans la Console Administrateur DPM.</span><span class="sxs-lookup"><span data-stu-id="35597-164">To recover an Exchange database, click **Recovery** in the DPM Administrator Console.</span></span>
2. <span data-ttu-id="35597-165">Localisez la base de données Exchange que vous souhaitez récupérer.</span><span class="sxs-lookup"><span data-stu-id="35597-165">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="35597-166">Sélectionnez un point de récupération en ligne dans la liste déroulante *Heure de récupération* .</span><span class="sxs-lookup"><span data-stu-id="35597-166">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="35597-167">Cliquez sur **Récupérer** pour lancer **l’Assistant Récupération**.</span><span class="sxs-lookup"><span data-stu-id="35597-167">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="35597-168">Pour les points de récupération en ligne, il existe cinq types de récupération :</span><span class="sxs-lookup"><span data-stu-id="35597-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="35597-169">**Récupérer à l’emplacement d’origine du serveur Exchange :** les données seront récupérées sur le serveur Exchange d’origine.</span><span class="sxs-lookup"><span data-stu-id="35597-169">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="35597-170">**Récupérer vers une autre base de données sur un serveur Exchange :** les données seront récupérées dans une autre base de données sur un autre serveur Exchange.</span><span class="sxs-lookup"><span data-stu-id="35597-170">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="35597-171">**Récupérer dans une base de données de récupération :** les données seront récupérées dans une base de données de récupération Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="35597-171">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="35597-172">**Copier dans un dossier réseau :** les données seront récupérées dans un dossier réseau.</span><span class="sxs-lookup"><span data-stu-id="35597-172">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="35597-173">**Copier sur bande :** si une bibliothèque de bandes ou un lecteur de bandes autonome est attaché(e) et configuré(e) sur le serveur DPM, le point de récupération sera copié sur une bande disponible.</span><span class="sxs-lookup"><span data-stu-id="35597-173">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on the DPM server, the recovery point will be copied to a free tape.</span></span>

    ![Choisir la réplication en ligne](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="35597-175">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="35597-175">Next steps</span></span>
* [<span data-ttu-id="35597-176">Azure Backup - Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="35597-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
