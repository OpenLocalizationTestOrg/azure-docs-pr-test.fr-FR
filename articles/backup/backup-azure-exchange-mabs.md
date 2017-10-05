---
title: "Sauvegarder un serveur Exchange dans une sauvegarde Microsoft Azure avec le serveur de sauvegarde Azure | Microsoft Docs"
description: "Découvrez comment sauvegarder un serveur Exchange dans une sauvegarde Microsoft Azure avec le serveur de sauvegarde Azure."
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
ms.openlocfilehash: 60b784fd00013c2b9504f8635c6b5c4c592563be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-azure-backup-server"></a><span data-ttu-id="12ba4-103">Sauvegarder un serveur Exchange dans une sauvegarde Microsoft Azure avec le serveur de sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="12ba4-103">Back up an Exchange server to Azure Backup with Azure Backup Server</span></span>
<span data-ttu-id="12ba4-104">Cet article explique comment configurer un serveur de sauvegarde Azure pour sauvegarder un serveur Microsoft Exchange dans une sauvegarde Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="12ba4-104">This article describes how to configure Microsoft Azure Backup Server (MABS) to back up a Microsoft Exchange server to Azure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="12ba4-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="12ba4-105">Prerequisites</span></span>
<span data-ttu-id="12ba4-106">Avant de continuer, assurez-vous que le serveur de sauvegarde Azure est [installé et prêt](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="12ba4-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="12ba4-107">Agent de protection du serveur de sauvegarde Azure</span><span class="sxs-lookup"><span data-stu-id="12ba4-107">MABS protection agent</span></span>
<span data-ttu-id="12ba4-108">Pour installer l’agent de protection du serveur de sauvegarde Azure sur le serveur Exchange, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="12ba4-108">To install the MABS protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="12ba4-109">Assurez-vous que les pare-feux sont correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="12ba4-109">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="12ba4-110">Consultez la page [Configuration d’exceptions de pare-feu pour l’agent](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="12ba4-110">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="12ba4-111">Installez l’agent sur le serveur Exchange, en cliquant sur **Gestion > Agents > Installer** dans la console administrateur du serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="12ba4-111">Install the agent on the Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="12ba4-112">Pour obtenir des instructions détaillées, consultez la page [Installation de l’agent de protection du serveur de sauvegarde Azure](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="12ba4-112">See [Install the MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="12ba4-113">Créer un groupe de protection pour le serveur Exchange</span><span class="sxs-lookup"><span data-stu-id="12ba4-113">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="12ba4-114">Dans la console administrateur du serveur de sauvegarde Azure, cliquez sur **Protection**, puis sélectionnez **Nouveau** dans la barre d’outils pour ouvrir l’assistant **Créer un groupe de protection**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-114">In the MABS Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="12ba4-115">Dans l’écran d’**accueil** de l’assistant, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-115">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="12ba4-116">Dans l’écran **Sélectionner le type de groupe de protection**, sélectionnez **Serveurs**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-116">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="12ba4-117">Sélectionnez la base de données du serveur Exchange que vous souhaitez protéger, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-117">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="12ba4-118">Si vous protégez Exchange 2013, vérifiez les [Conditions préalables pour Exchange 2013](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="12ba4-118">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="12ba4-119">Dans l’exemple suivant, la base de données Exchange 2010 est sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="12ba4-119">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Sélectionner les membres du groupe](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="12ba4-121">Sélectionnez la méthode de protection des données.</span><span class="sxs-lookup"><span data-stu-id="12ba4-121">Select the data protection method.</span></span>

    <span data-ttu-id="12ba4-122">Attribuez un nom au groupe de protection, puis sélectionnez les deux options suivantes :</span><span class="sxs-lookup"><span data-stu-id="12ba4-122">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="12ba4-123">Je souhaite une protection à court terme à l’aide de Disque.</span><span class="sxs-lookup"><span data-stu-id="12ba4-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="12ba4-124">Je voudrais une protection en ligne.</span><span class="sxs-lookup"><span data-stu-id="12ba4-124">I want online protection.</span></span>
6. <span data-ttu-id="12ba4-125">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-125">Click **Next**.</span></span>
7. <span data-ttu-id="12ba4-126">Sélectionnez l’option **Exécuter Eseutil pour vérifier l’intégrité des données** si vous souhaitez vérifier l’intégrité des bases de données Exchange Server.</span><span class="sxs-lookup"><span data-stu-id="12ba4-126">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="12ba4-127">Une fois cette option sélectionnée, une vérification de la cohérence de sauvegarde s’exécute sur le serveur de sauvegarde Azure, afin d’éviter le trafic d’E/S généré lors de l’exécution de la commande **eseutil** sur le serveur Exchange.</span><span class="sxs-lookup"><span data-stu-id="12ba4-127">After you select this option, backup consistency checking will be run on MABS to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="12ba4-128">Pour utiliser cette option, vous devez copier les fichiers Ese.dll et Eseutil.exe dans le répertoire C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin sur le serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="12ba4-128">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on the MAB server.</span></span> <span data-ttu-id="12ba4-129">Dans le cas contraire, l’erreur suivante est déclenchée : </span><span class="sxs-lookup"><span data-stu-id="12ba4-129">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="12ba4-130">![erreur eseutil](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="12ba4-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="12ba4-131">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-131">Click **Next**.</span></span>
9. <span data-ttu-id="12ba4-132">Sélectionnez la base de données pour **Sauvegarde de copie**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-132">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="12ba4-133">Si vous ne sélectionnez pas « Sauvegarde complète » pour au moins une copie DAG d’une base de données, les journaux ne seront pas tronqués.</span><span class="sxs-lookup"><span data-stu-id="12ba4-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="12ba4-134">Configurez les objectifs de **Sauvegarde à court terme**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-134">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="12ba4-135">Vérifiez l’espace disque disponible, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-135">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="12ba4-136">Sélectionnez l’heure à laquelle le serveur de sauvegarde Azure doit créer la réplication initiale, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-136">Select the time at which the MAB Server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="12ba4-137">Sélectionnez les options de vérification de cohérence, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-137">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="12ba4-138">Choisissez la base de données que vous souhaitez sauvegarder sur Azure, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-138">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="12ba4-139">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="12ba4-139">For example:</span></span>

    ![Spécifier les données de protection en ligne](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="12ba4-141">Définissez la planification pour **Azure Backup**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-141">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="12ba4-142">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="12ba4-142">For example:</span></span>

    ![Spécifier la planification de sauvegarde en ligne](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="12ba4-144">Notez que les points de récupération en ligne sont basés sur des points de récupération complète express.</span><span class="sxs-lookup"><span data-stu-id="12ba4-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="12ba4-145">Par conséquent, vous devez planifier le point de récupération en ligne après l’heure spécifiée pour le point de récupération complète express.</span><span class="sxs-lookup"><span data-stu-id="12ba4-145">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="12ba4-146">Configurer la stratégie de rétention pour **Azure Backup**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-146">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="12ba4-147">Choisissez une option de réplication en ligne, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="12ba4-148">Si vous disposez d’une base de données volumineuse, la création de la sauvegarde initiale sur le réseau peut prendre un long moment.</span><span class="sxs-lookup"><span data-stu-id="12ba4-148">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="12ba4-149">Pour éviter ce problème, vous pouvez créer une sauvegarde hors connexion.</span><span class="sxs-lookup"><span data-stu-id="12ba4-149">To avoid this issue, you can create an offline backup.</span></span>  

    ![Spécifier la stratégie de rétention en ligne](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="12ba4-151">Confirmez les paramètres, puis cliquez sur **Créer un groupe**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-151">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="12ba4-152">Cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-152">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="12ba4-153">Récupérer la base de données Exchange</span><span class="sxs-lookup"><span data-stu-id="12ba4-153">Recover the Exchange database</span></span>
1. <span data-ttu-id="12ba4-154">Pour récupérer une base de données Exchange, cliquez sur **Récupération** dans la console administrateur du serveur de sauvegarde Azure.</span><span class="sxs-lookup"><span data-stu-id="12ba4-154">To recover an Exchange database, click **Recovery** in the MABS Administrator Console.</span></span>
2. <span data-ttu-id="12ba4-155">Localisez la base de données Exchange que vous souhaitez récupérer.</span><span class="sxs-lookup"><span data-stu-id="12ba4-155">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="12ba4-156">Sélectionnez un point de récupération en ligne dans la liste déroulante *Heure de récupération* .</span><span class="sxs-lookup"><span data-stu-id="12ba4-156">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="12ba4-157">Cliquez sur **Récupérer** pour lancer **l’Assistant Récupération**.</span><span class="sxs-lookup"><span data-stu-id="12ba4-157">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="12ba4-158">Pour les points de récupération en ligne, il existe cinq types de récupération :</span><span class="sxs-lookup"><span data-stu-id="12ba4-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="12ba4-159">**Récupérer à l’emplacement d’origine du serveur Exchange :** les données seront récupérées sur le serveur Exchange d’origine.</span><span class="sxs-lookup"><span data-stu-id="12ba4-159">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="12ba4-160">**Récupérer vers une autre base de données sur un serveur Exchange :** les données seront récupérées dans une autre base de données sur un autre serveur Exchange.</span><span class="sxs-lookup"><span data-stu-id="12ba4-160">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="12ba4-161">**Récupérer dans une base de données de récupération :** les données seront récupérées dans une base de données de récupération Exchange (RDB).</span><span class="sxs-lookup"><span data-stu-id="12ba4-161">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="12ba4-162">**Copier dans un dossier réseau :** les données seront récupérées dans un dossier réseau.</span><span class="sxs-lookup"><span data-stu-id="12ba4-162">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="12ba4-163">**Copier sur bande :** si une bibliothèque de bandes ou un lecteur de bandes autonome sont attachés et configurés sur le serveur de sauvegarde Azure, le point de récupération est copié sur une bande disponible.</span><span class="sxs-lookup"><span data-stu-id="12ba4-163">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, the recovery point will be copied to a free tape.</span></span>

    ![Choisir la réplication en ligne](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="12ba4-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12ba4-165">Next steps</span></span>
* [<span data-ttu-id="12ba4-166">Azure Backup - Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="12ba4-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)
