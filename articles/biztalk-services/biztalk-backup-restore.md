---
title: "Créer et restaurer une sauvegarde dans BizTalk Services | Microsoft Docs"
description: "BizTalk Services offre des fonctionnalités de sauvegarde et de restauration. Apprenez à créer et à restaurer une sauvegarde et à déterminer les éléments sauvegardés. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c55d1ab124441c42101b4ad60924a9ea28231408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="027eb-105">Sauvegarde et restauration de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="027eb-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="027eb-106">Azure BizTalk Services offre des fonctionnalités de sauvegarde et de restauration.</span><span class="sxs-lookup"><span data-stu-id="027eb-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="027eb-107">Cette rubrique montre comment effectuer une sauvegarde et une restauration BizTalk Services à l’aide du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="027eb-107">This topic describes how to backup and restore BizTalk Services using the Azure classic portal.</span></span>

<span data-ttu-id="027eb-108">Vous pouvez également utiliser l' [API REST BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=325584)pour sauvegarder BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="027eb-108">You can also back up BizTalk Services using the [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="027eb-109">Les connexions hybrides NE sont PAS sauvegardées, quelle que soit l’édition.</span><span class="sxs-lookup"><span data-stu-id="027eb-109">Hybrid Connections are NOT backed up, regardless of the Edition.</span></span> <span data-ttu-id="027eb-110">Vous devez recréer vos connexions hybrides.</span><span class="sxs-lookup"><span data-stu-id="027eb-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="027eb-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="027eb-111">Before you Begin</span></span>
* <span data-ttu-id="027eb-112">Il se peut que les fonctionnalités de sauvegarde et de restauration ne soient pas disponibles dans toutes les éditions.</span><span class="sxs-lookup"><span data-stu-id="027eb-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="027eb-113">Consultez [BizTalk Services : tableau comparatif des éditions](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="027eb-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="027eb-114">À l’aide du portail Azure Classic, vous pouvez créer une sauvegarde à la demande ou planifiée.</span><span class="sxs-lookup"><span data-stu-id="027eb-114">Using the Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="027eb-115">Le contenu des sauvegardes peut être restauré vers le même service BizTalk ou vers un nouveau service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="027eb-115">Backup content can be restored to the same BizTalk Service or to a new BizTalk Service.</span></span> <span data-ttu-id="027eb-116">Pour restaurer le service BizTalk à l'aide du même nom, le service BizTalk existant doit être supprimé et le nom doit être disponible.</span><span class="sxs-lookup"><span data-stu-id="027eb-116">To restore the BizTalk Service using the same name, the existing BizTalk Service must be deleted and the name must be available.</span></span> <span data-ttu-id="027eb-117">Après avoir supprimé un service BizTalk, la disponibilité du même nom peut prendre du temps.</span><span class="sxs-lookup"><span data-stu-id="027eb-117">After you delete a BizTalk Service, it can take longer time than wanted for the same name to be available.</span></span> <span data-ttu-id="027eb-118">Si vous ne pouvez pas attendre que le même nom soit disponible, restaurez vers un nouveau service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="027eb-118">If you cannot wait for the same name to be available, then restore to a new BizTalk Service.</span></span>
* <span data-ttu-id="027eb-119">BizTalk Services peut être restauré vers la même édition ou une édition supérieure.</span><span class="sxs-lookup"><span data-stu-id="027eb-119">BizTalk Services can be restored to the same edition or a higher edition.</span></span> <span data-ttu-id="027eb-120">La restauration de BizTalk Services vers une édition inférieure, à partir de la sauvegarde créée, n'est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="027eb-120">Restoring BizTalk Services to a lower edition, from when the backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="027eb-121">Par exemple, une sauvegarde à l'aide de l'édition De base peut être restaurée vers l'édition Premium</span><span class="sxs-lookup"><span data-stu-id="027eb-121">For example, a backup using the Basic Edition can be restored to the Premium Edition.</span></span> <span data-ttu-id="027eb-122">alors qu'une sauvegarde dans l'autre sens est impossible.</span><span class="sxs-lookup"><span data-stu-id="027eb-122">A backup using the Premium Edition cannot be restored to the Standard Edition.</span></span>
* <span data-ttu-id="027eb-123">Les numéros de contrôle EDI sont sauvegardés pour assurer la continuité des numéros de contrôle.</span><span class="sxs-lookup"><span data-stu-id="027eb-123">The EDI Control numbers are backed up to maintain continuity of the control numbers.</span></span> <span data-ttu-id="027eb-124">Si des messages sont traités après la dernière sauvegarde, la restauration du contenu de cette sauvegarde peut entraîner des numéros de contrôle en double.</span><span class="sxs-lookup"><span data-stu-id="027eb-124">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="027eb-125">Si un lot contient des messages actifs, traitez-le **avant** d'effectuer une sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="027eb-125">If a batch has active messages, process the batch **before** running a backup.</span></span> <span data-ttu-id="027eb-126">Lors de la création d'une sauvegarde (à la demande ou planifiée), les messages contenus dans des lots ne sont jamais stockés.</span><span class="sxs-lookup"><span data-stu-id="027eb-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="027eb-127">**En cas de sauvegarde présentant des messages actifs dans un lot, ceux-ci ne sont pas sauvegardés et sont donc perdus.**</span><span class="sxs-lookup"><span data-stu-id="027eb-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="027eb-128">Facultatif : dans le portail BizTalk Services, arrêtez toutes les opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="027eb-128">Optional: In the BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="027eb-129">Création d'une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="027eb-129">Create a backup</span></span>
<span data-ttu-id="027eb-130">Une sauvegarde peut être effectuée à tout moment et vous la contrôlez complètement.</span><span class="sxs-lookup"><span data-stu-id="027eb-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="027eb-131">Cette section répertorie les étapes à suivre pour créer des sauvegardes à l’aide du portail Azure Classic :</span><span class="sxs-lookup"><span data-stu-id="027eb-131">This section lists the steps to create backups using the Azure classic portal, including:</span></span>

[<span data-ttu-id="027eb-132">Sauvegarde à la demande</span><span class="sxs-lookup"><span data-stu-id="027eb-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="027eb-133">Planification d'une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="027eb-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="027eb-134"><a name="backupnow"></a>Sauvegarde à la demande</span><span class="sxs-lookup"><span data-stu-id="027eb-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="027eb-135">Dans le portail Azure Classic, sélectionnez **BizTalk Services**, puis le service BizTalk que vous souhaitez sauvegarder.</span><span class="sxs-lookup"><span data-stu-id="027eb-135">In the Azure classic portal, select **BizTalk Services**, and then select the BizTalk Service you want to backup.</span></span>
2. <span data-ttu-id="027eb-136">Sous l’onglet **Tableau de bord**, sélectionnez **Sauvegarder** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="027eb-136">In the **Dashboard** tab, select **Back up** at the bottom of the page.</span></span>
3. <span data-ttu-id="027eb-137">Entrez un nom de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="027eb-137">Enter a backup name.</span></span> <span data-ttu-id="027eb-138">Par exemple, entrez *monServiceBizTalk*BU*Date*.</span><span class="sxs-lookup"><span data-stu-id="027eb-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="027eb-139">Choisissez un compte de stockage d'objets blob et sélectionnez la coche pour démarrer la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="027eb-139">Choose a blob storage account and select the checkmark to start the backup.</span></span>

<span data-ttu-id="027eb-140">Une fois la sauvegarde terminée, un conteneur portant le nom de sauvegarde indiqué est créé dans le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="027eb-140">Once the backup completes, a container with the backup name you enter is created in the storage account.</span></span> <span data-ttu-id="027eb-141">Ce conteneur comprend la configuration de sauvegarde de votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="027eb-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="027eb-142"><a name="backupschedule"></a>Planification d'une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="027eb-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="027eb-143">Dans le Portail Azure Classic, sélectionnez **BizTalk Services**, puis le nom du service BizTalk pour lequel vous souhaitez planifier la sauvegarde et enfin l’onglet **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="027eb-143">In the Azure classic portal, select **BizTalk Services**, select the BizTalk Service name you want to schedule the backup, and then select the **Configure** tab.</span></span>
2. <span data-ttu-id="027eb-144">Définissez **État de la sauvegarde** sur **Automatique**.</span><span class="sxs-lookup"><span data-stu-id="027eb-144">Set the **Backup Status** to **Automatic**.</span></span> 
3. <span data-ttu-id="027eb-145">Sélectionnez le **Compte de stockage** dans lequel stocker la sauvegarde, puis entrez la **Fréquence** de création des sauvegardes et la durée pendant laquelle vous souhaitez les conserver (**Jours de rétention**) :</span><span class="sxs-lookup"><span data-stu-id="027eb-145">Select the **Storage Account** to store the backup, enter the **Frequency** to create the backups, and how long to keep the backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="027eb-146">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="027eb-146">**Notes**</span></span>     
   
   * <span data-ttu-id="027eb-147">Dans **Jours de rétention**, la période de rétention doit être supérieure à la fréquence des sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="027eb-147">In **Retention Days**, the retention period must be greater than the backup frequency.</span></span>
   * <span data-ttu-id="027eb-148">Sélectionnez **Conserver toujours au moins une sauvegarde**, même si le délai de rétention est dépassé.</span><span class="sxs-lookup"><span data-stu-id="027eb-148">Select **Always keep at least one backup**, even if it is past the retention period.</span></span>
4. <span data-ttu-id="027eb-149">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="027eb-149">Select **Save**.</span></span>

<span data-ttu-id="027eb-150">Lors de l'exécution d'une tâche de sauvegarde planifiée, un conteneur est créé (pour stocker les données de sauvegarde) dans le compte de stockage que vous avez indiqué.</span><span class="sxs-lookup"><span data-stu-id="027eb-150">When a scheduled backup job runs, it creates a container (to store backup data) in the storage account you entered.</span></span> <span data-ttu-id="027eb-151">Le nom du conteneur se présente comme suit : *Service BizTalk nom-date-heure*.</span><span class="sxs-lookup"><span data-stu-id="027eb-151">The name of the container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="027eb-152">Si le tableau de bord du service BizTalk indique l'état **Échec** :</span><span class="sxs-lookup"><span data-stu-id="027eb-152">If the BizTalk Service dashboard shows a **Failed** status:</span></span>

![Statut de la dernière sauvegarde planifiée][BackupStatus] 

<span data-ttu-id="027eb-154">Le lien ouvre les journaux des opérations des services de gestion pour vous aider à résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="027eb-154">The link opens the Management Services Operation Logs to help troubleshoot.</span></span> <span data-ttu-id="027eb-155">Consultez [BizTalk Services : résolution des problèmes à l'aide des journaux des opérations](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="027eb-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="027eb-156">Restore</span><span class="sxs-lookup"><span data-stu-id="027eb-156">Restore</span></span>
<span data-ttu-id="027eb-157">Vous pouvez restaurer des sauvegardes depuis le portail Azure Classic ou l’ [API REST Restaurer le service BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="027eb-157">You can restore backups from the Azure classic portal or from the [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="027eb-158">Cette section répertorie les étapes à suivre pour restaurer une sauvegarde à l’aide du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="027eb-158">This section lists the steps to restore using the classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="027eb-159">Avant de restaurer une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="027eb-159">Before restoring a backup</span></span>
* <span data-ttu-id="027eb-160">De nouveaux magasins de suivi, d'archivage et de surveillance peuvent être spécifiés lors de la restauration d'un service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="027eb-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="027eb-161">Les mêmes données de runtime EDI sont restaurées.</span><span class="sxs-lookup"><span data-stu-id="027eb-161">The same EDI Runtime data is restored.</span></span> <span data-ttu-id="027eb-162">La sauvegarde du runtime EDI stocke les numéros de contrôle.</span><span class="sxs-lookup"><span data-stu-id="027eb-162">The EDI Runtime backup stores the control numbers.</span></span> <span data-ttu-id="027eb-163">Les numéros de contrôle restaurés apparaissent en séquence depuis le moment de la sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="027eb-163">The restored control numbers are in sequence from the time of the backup.</span></span> <span data-ttu-id="027eb-164">Si des messages sont traités après la dernière sauvegarde, la restauration du contenu de cette sauvegarde peut entraîner des numéros de contrôle en double.</span><span class="sxs-lookup"><span data-stu-id="027eb-164">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="027eb-165">Restauration d'une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="027eb-165">Restore a backup</span></span>
1. <span data-ttu-id="027eb-166">Dans le Portail Azure Classic, sélectionnez **Nouveau** > **App Services** > **Service BizTalk** > **Restaurer** :</span><span class="sxs-lookup"><span data-stu-id="027eb-166">In the Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Restauration d'une sauvegarde][Restore]
2. <span data-ttu-id="027eb-168">Dans **URL de sauvegarde**, sélectionnez l'icône de dossier et développez le compte de stockage Azure qui stocke la sauvegarde de la configuration du service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="027eb-168">In **Backup URL**, select the folder icon and expand the Azure storage account that stores the BizTalk Service configuration backup.</span></span> <span data-ttu-id="027eb-169">Développez le conteneur, puis dans le volet droit, sélectionnez le fichier .txt de sauvegarde correspondant.</span><span class="sxs-lookup"><span data-stu-id="027eb-169">Expand the container and in the right pane, select the corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="027eb-170">Sélectionnez **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="027eb-170">Select **Open**.</span></span>
3. <span data-ttu-id="027eb-171">Dans la page **Restaurer le service BizTalk**, entrez le **Nom du service BizTalk**, puis vérifiez **l’URL de domaine**, **l’Édition** et la **Région** du service BizTalk restauré.</span><span class="sxs-lookup"><span data-stu-id="027eb-171">On the **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify the **Domain URL**, **Edition**, and **Region** for the restored BizTalk Service.</span></span> <span data-ttu-id="027eb-172">**Créer une instance de base de données SQL** pour la base de données de suivi :</span><span class="sxs-lookup"><span data-stu-id="027eb-172">**Create a new SQL database instance** for the tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="027eb-173">Sélectionnez la flèche Suivant.</span><span class="sxs-lookup"><span data-stu-id="027eb-173">Select the next arrow.</span></span>
4. <span data-ttu-id="027eb-174">Vérifiez le nom de la base de données SQL, entrez le serveur physique sur lequel la base de données SQL sera créée, ainsi qu'un nom d'utilisateur/mot de passe pour ce serveur.</span><span class="sxs-lookup"><span data-stu-id="027eb-174">Verify the name of the SQL database, enter the physical server where the SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="027eb-175">Si vous souhaitez configurer l’édition, la taille et d’autres propriétés de la base de données SQL, sélectionnez **Configurer les paramètres avancés de la base de données**.</span><span class="sxs-lookup"><span data-stu-id="027eb-175">If you want to configure the SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="027eb-176">Sélectionnez la flèche Suivant.</span><span class="sxs-lookup"><span data-stu-id="027eb-176">Select the next arrow.</span></span>

1. <span data-ttu-id="027eb-177">Créez un compte de stockage ou spécifiez un compte de stockage existant pour le service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="027eb-177">Create a new storage account or enter an existing storage account for the BizTalk Service.</span></span>
2. <span data-ttu-id="027eb-178">Cliquez sur la coche pour démarrer la restauration.</span><span class="sxs-lookup"><span data-stu-id="027eb-178">Select the checkmark to start the restore.</span></span>

<span data-ttu-id="027eb-179">Une fois la restauration terminée, un nouveau service BizTalk est répertorié comme étant dans un état interrompu sur la page BizTalk Services du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="027eb-179">Once the restoration successfully completes, a new BizTalk Service is listed in a suspended state on the BizTalk Services page in the Azure classic portal.</span></span>

### <span data-ttu-id="027eb-180"><a name="postrestore"></a>Après avoir restauré une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="027eb-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="027eb-181">Le service BizTalk est systématiquement restauré dans un état **Suspendu** .</span><span class="sxs-lookup"><span data-stu-id="027eb-181">The BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="027eb-182">Dans cet état, vous pouvez apporter des modifications à la configuration avant que le nouvel environnement ne soit fonctionnel :</span><span class="sxs-lookup"><span data-stu-id="027eb-182">In this state, you can make any configuration changes before the new environment is functional, including:</span></span>

* <span data-ttu-id="027eb-183">Si vous avez créé des applications de service BizTalk à l'aide du Kit de développement logiciel (SDK) Azure BizTalk Services, vous devrez peut-être mettre à jour les informations d'identification Access Control (ACS) qui s'y rapportent pour qu'elles fonctionnent dans l'environnement restauré.</span><span class="sxs-lookup"><span data-stu-id="027eb-183">If you created BizTalk Service applications using the Azure BizTalk Services SDK, you may need to to update the Access Control (ACS) credentials in those applications to work with the restored environment.</span></span>
* <span data-ttu-id="027eb-184">Vous restaurez un service BizTalk pour répliquer un environnement de service BizTalk existant.</span><span class="sxs-lookup"><span data-stu-id="027eb-184">You restore a BizTalk Service to replicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="027eb-185">Dans ce cas de figure, s'il existe des contrats configurés dans le portail BizTalk Services d'origine utilisant un dossier FTP source, vous devrez peut-être mettre à jour les contrats de l'environnement récemment restauré de manière à utiliser un autre dossier FTP source.</span><span class="sxs-lookup"><span data-stu-id="027eb-185">In this situation, if there are agreements configured in the original BizTalk Services portal that use a source FTP folder, you may need to update the agreements in the newly restored environment to use a different source FTP folder.</span></span> <span data-ttu-id="027eb-186">Sinon, vous risquez de vous retrouver avec deux contrats différents tentant d'extraire le même message.</span><span class="sxs-lookup"><span data-stu-id="027eb-186">Otherwise, there may be two different agreements trying to pull the same message.</span></span>
* <span data-ttu-id="027eb-187">Si vous avez procédé à la restauration pour plusieurs environnements de service BizTalk, veillez à cibler l'environnement approprié dans les applications Visual Studio, applets de commande PowerShell, API REST ou API OM du portail de gestion du partenaire commercial.</span><span class="sxs-lookup"><span data-stu-id="027eb-187">If you restored to have multiple BizTalk Service environments, make sure you target the correct environment in the Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="027eb-188">Il est recommandé de configurer des sauvegardes automatisées dans l'environnement du service BizTalk récemment restauré.</span><span class="sxs-lookup"><span data-stu-id="027eb-188">It's a good practice to configure automated backups on the newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="027eb-189">Pour démarrer le service BizTalk dans le portail Azure Classic, sélectionnez le service BizTalk restauré, puis **Reprendre** dans la barre des tâches.</span><span class="sxs-lookup"><span data-stu-id="027eb-189">To start the BizTalk Service in the Azure classic portal, select the restored BizTalk Service and select **Resume** in the task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="027eb-190">Éléments sauvegardés</span><span class="sxs-lookup"><span data-stu-id="027eb-190">What gets backed up</span></span>
<span data-ttu-id="027eb-191">Dans le cadre d'une sauvegarde, les éléments suivants sont sauvegardés :</span><span class="sxs-lookup"><span data-stu-id="027eb-191">When a backup is created, the following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="027eb-192">Éléments sauvegardés</span><span class="sxs-lookup"><span data-stu-id="027eb-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="027eb-193">
 <strong>Portail Azure BizTalk Services</strong></span><span class="sxs-lookup"><span data-stu-id="027eb-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="027eb-194">Configuration et exécution</span><span class="sxs-lookup"><span data-stu-id="027eb-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="027eb-195">Détails du partenaire et du profil</span><span class="sxs-lookup"><span data-stu-id="027eb-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="027eb-196">Contrats partenaires</span><span class="sxs-lookup"><span data-stu-id="027eb-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="027eb-197">Assemblys personnalisés déployés</span><span class="sxs-lookup"><span data-stu-id="027eb-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="027eb-198">Ponts déployés</span><span class="sxs-lookup"><span data-stu-id="027eb-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="027eb-199">Certificats</span><span class="sxs-lookup"><span data-stu-id="027eb-199">Certificates</span></span></li>
<li><span data-ttu-id="027eb-200">Transformations déployées</span><span class="sxs-lookup"><span data-stu-id="027eb-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="027eb-201">Pipelines</span><span class="sxs-lookup"><span data-stu-id="027eb-201">Pipelines</span></span></li>
<li><span data-ttu-id="027eb-202">Modèles créés et enregistrés dans le portail BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="027eb-202">Templates created and saved in the BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="027eb-203">Mappages X12 ST01 et GS01</span><span class="sxs-lookup"><span data-stu-id="027eb-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="027eb-204">Numéros de contrôle (EDI)</span><span class="sxs-lookup"><span data-stu-id="027eb-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="027eb-205">Valeurs MIC des messages AS2</span><span class="sxs-lookup"><span data-stu-id="027eb-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="027eb-206">
 <strong>Azure BizTalk Service</strong></span><span class="sxs-lookup"><span data-stu-id="027eb-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="027eb-207">Certificat SSL</span><span class="sxs-lookup"><span data-stu-id="027eb-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="027eb-208">Données du certificat SSL</span><span class="sxs-lookup"><span data-stu-id="027eb-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="027eb-209">Mot de passe du certificat SSL</span><span class="sxs-lookup"><span data-stu-id="027eb-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="027eb-210">Paramètres du service BizTalk</span><span class="sxs-lookup"><span data-stu-id="027eb-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="027eb-211">Nombre d'unités mises à l'échelle</span><span class="sxs-lookup"><span data-stu-id="027eb-211">Scale unit count</span></span></li>
<li><span data-ttu-id="027eb-212">Édition</span><span class="sxs-lookup"><span data-stu-id="027eb-212">Edition</span></span></li>
<li><span data-ttu-id="027eb-213">Version du produit</span><span class="sxs-lookup"><span data-stu-id="027eb-213">Product Version</span></span></li>
<li><span data-ttu-id="027eb-214">Région/centre de données</span><span class="sxs-lookup"><span data-stu-id="027eb-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="027eb-215">Espace de noms et clé Access Control Service (ACS)</span><span class="sxs-lookup"><span data-stu-id="027eb-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="027eb-216">Chaîne de connexion à la base de données de suivi</span><span class="sxs-lookup"><span data-stu-id="027eb-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="027eb-217">Chaîne de connexion au compte de stockage d'archive</span><span class="sxs-lookup"><span data-stu-id="027eb-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="027eb-218">Chaîne de connexion au compte de stockage de surveillance</span><span class="sxs-lookup"><span data-stu-id="027eb-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="027eb-219">
 <strong>Autres éléments</strong></span><span class="sxs-lookup"><span data-stu-id="027eb-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="027eb-220">Base de données des suivis</span><span class="sxs-lookup"><span data-stu-id="027eb-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="027eb-221">Lors de la création du service BizTalk, les détails relatifs à la base de données de suivi sont entrés, y compris le serveur de la base de données SQL Azure et le nom de la base de données de suivi.</span><span class="sxs-lookup"><span data-stu-id="027eb-221">When the BizTalk Service is created, the Tracking Database details are entered, including the Azure SQL Database Server and the Tracking Database name.</span></span> <span data-ttu-id="027eb-222">La base de données de suivi n'est pas automatiquement sauvegardée.</span><span class="sxs-lookup"><span data-stu-id="027eb-222">The Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="027eb-223">
<strong>Important</strong></span><span class="sxs-lookup"><span data-stu-id="027eb-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="027eb-224">Si la base de données de suivi est supprimée et qu'elle doit être récupérée, une sauvegarde précédente est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="027eb-224">If the Tracking Database is deleted and the database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="027eb-225">En l'absence de sauvegarde précédente, la base de données de suivi et les données associées ne pourront pas être récupérées.</span><span class="sxs-lookup"><span data-stu-id="027eb-225">If a backup does not exist, the Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="027eb-226">Dans ce cas, créez une base de données de suivi portant le même nom.</span><span class="sxs-lookup"><span data-stu-id="027eb-226">In this situation, create a new Tracking Database with the same database name.</span></span> <span data-ttu-id="027eb-227">La géo-réplication est recommandée.</span><span class="sxs-lookup"><span data-stu-id="027eb-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="027eb-228">Suivant</span><span class="sxs-lookup"><span data-stu-id="027eb-228">Next</span></span>
<span data-ttu-id="027eb-229">Pour créer des services Azure BizTalk Services dans le portail Azure Classic, accédez à [BizTalk Services : approvisionnement à l’aide du portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="027eb-229">To create Azure BizTalk Services in the Azure classic portal, go to [BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="027eb-230">Pour commencer à créer des applications, consultez la page [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="027eb-230">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="027eb-231">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="027eb-231">See Also</span></span>
* [<span data-ttu-id="027eb-232">Sauvegarde d'un service BizTalk</span><span class="sxs-lookup"><span data-stu-id="027eb-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="027eb-233">Restauration d'un service BizTalk depuis une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="027eb-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="027eb-234">Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="027eb-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="027eb-235">BizTalk Services : approvisionnement à l’aide du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="027eb-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="027eb-236">Tableau comparatif des états d'approvisionnement BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="027eb-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="027eb-237">Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="027eb-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="027eb-238">Limitation dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="027eb-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="027eb-239">Nom et clé de l'émetteur dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="027eb-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="027eb-240">Utilisation du Kit de développement logiciel (SDK) Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="027eb-240">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

