---
title: aaaCreate et restaurer une sauvegarde dans BizTalk Services | Documents Microsoft
description: "BizTalk Services offre des fonctionnalités de sauvegarde et de restauration. Découvrez comment toocreate déterminer ce que sauvegarder et restaurer une sauvegarde. MABS, WABS"
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
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="607e5-105">Sauvegarde et restauration de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="607e5-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="607e5-106">Azure BizTalk Services offre des fonctionnalités de sauvegarde et de restauration.</span><span class="sxs-lookup"><span data-stu-id="607e5-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="607e5-107">Cette rubrique décrit comment toobackup et restauration des Services BizTalk à l’aide de hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="607e5-107">This topic describes how toobackup and restore BizTalk Services using hello Azure classic portal.</span></span>

<span data-ttu-id="607e5-108">Vous pouvez également sauvegarder les Services BizTalk à l’aide de hello [API REST des Services BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="607e5-108">You can also back up BizTalk Services using hello [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="607e5-109">Connexions hybrides ne sont pas sauvegardées, quel que soit l’édition de hello.</span><span class="sxs-lookup"><span data-stu-id="607e5-109">Hybrid Connections are NOT backed up, regardless of hello Edition.</span></span> <span data-ttu-id="607e5-110">Vous devez recréer vos connexions hybrides.</span><span class="sxs-lookup"><span data-stu-id="607e5-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="607e5-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="607e5-111">Before you Begin</span></span>
* <span data-ttu-id="607e5-112">Il se peut que les fonctionnalités de sauvegarde et de restauration ne soient pas disponibles dans toutes les éditions.</span><span class="sxs-lookup"><span data-stu-id="607e5-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="607e5-113">Consultez [BizTalk Services : tableau comparatif des éditions](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="607e5-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="607e5-114">À l’aide de hello portail Azure classic, vous pouvez créer une sauvegarde à la demande ou créer une sauvegarde planifiée.</span><span class="sxs-lookup"><span data-stu-id="607e5-114">Using hello Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="607e5-115">Contenu de sauvegarde peut être restaurée toohello même BizTalk Service ou tooa nouveau BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="607e5-115">Backup content can be restored toohello same BizTalk Service or tooa new BizTalk Service.</span></span> <span data-ttu-id="607e5-116">toorestore hello BizTalk Service à l’aide de hello même nom, hello existant du BizTalk Service doit être supprimé et hello nom doit être disponible.</span><span class="sxs-lookup"><span data-stu-id="607e5-116">toorestore hello BizTalk Service using hello same name, hello existing BizTalk Service must be deleted and hello name must be available.</span></span> <span data-ttu-id="607e5-117">Après avoir supprimé un BizTalk Service, il peut prendre plus de temps que vous souhaitiez pour hello même toobe nom disponible.</span><span class="sxs-lookup"><span data-stu-id="607e5-117">After you delete a BizTalk Service, it can take longer time than wanted for hello same name toobe available.</span></span> <span data-ttu-id="607e5-118">Si vous ne pouvez pas attendre hello même nom toobe disponible, puis restaurer tooa nouveau BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="607e5-118">If you cannot wait for hello same name toobe available, then restore tooa new BizTalk Service.</span></span>
* <span data-ttu-id="607e5-119">Les Services BizTalk peut être restaurée toohello même édition ou une édition supérieure.</span><span class="sxs-lookup"><span data-stu-id="607e5-119">BizTalk Services can be restored toohello same edition or a higher edition.</span></span> <span data-ttu-id="607e5-120">Restauration des Services BizTalk tooa version inférieure, à partir de lorsque hello sauvegarde, n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="607e5-120">Restoring BizTalk Services tooa lower edition, from when hello backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="607e5-121">Par exemple, une sauvegarde à l’aide de hello que édition Basic peut être restaurée toohello édition Premium.</span><span class="sxs-lookup"><span data-stu-id="607e5-121">For example, a backup using hello Basic Edition can be restored toohello Premium Edition.</span></span> <span data-ttu-id="607e5-122">Une sauvegarde à l’aide de hello que Premium Edition ne peut pas être restaurée toohello Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="607e5-122">A backup using hello Premium Edition cannot be restored toohello Standard Edition.</span></span>
* <span data-ttu-id="607e5-123">numéros de contrôle EDI Hello sont sauvegardées de continuité des activités toomaintain hello des numéros de contrôle.</span><span class="sxs-lookup"><span data-stu-id="607e5-123">hello EDI Control numbers are backed up toomaintain continuity of hello control numbers.</span></span> <span data-ttu-id="607e5-124">Si les messages sont traités après la dernière sauvegarde de hello, la restauration ce contenu de la sauvegarde peut entraîner des numéros de contrôle en double.</span><span class="sxs-lookup"><span data-stu-id="607e5-124">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="607e5-125">Si un lot de messages actifs, traite le lot de hello **avant** une sauvegarde en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="607e5-125">If a batch has active messages, process hello batch **before** running a backup.</span></span> <span data-ttu-id="607e5-126">Lors de la création d'une sauvegarde (à la demande ou planifiée), les messages contenus dans des lots ne sont jamais stockés.</span><span class="sxs-lookup"><span data-stu-id="607e5-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="607e5-127">**En cas de sauvegarde présentant des messages actifs dans un lot, ceux-ci ne sont pas sauvegardés et sont donc perdus.**</span><span class="sxs-lookup"><span data-stu-id="607e5-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="607e5-128">Facultatif : Hello portail BizTalk Services, d’arrêter toutes les opérations de gestion.</span><span class="sxs-lookup"><span data-stu-id="607e5-128">Optional: In hello BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="607e5-129">Création d'une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="607e5-129">Create a backup</span></span>
<span data-ttu-id="607e5-130">Une sauvegarde peut être effectuée à tout moment et vous la contrôlez complètement.</span><span class="sxs-lookup"><span data-stu-id="607e5-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="607e5-131">Cette section répertorie les sauvegardes de toocreate hello étapes à l’aide de hello Azure classic portail, y compris :</span><span class="sxs-lookup"><span data-stu-id="607e5-131">This section lists hello steps toocreate backups using hello Azure classic portal, including:</span></span>

[<span data-ttu-id="607e5-132">Sauvegarde à la demande</span><span class="sxs-lookup"><span data-stu-id="607e5-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="607e5-133">Planification d'une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="607e5-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="607e5-134"><a name="backupnow"></a>Sauvegarde à la demande</span><span class="sxs-lookup"><span data-stu-id="607e5-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="607e5-135">Bonjour portail Azure classic, sélectionnez **BizTalk Services**, et puis sélectionnez hello BizTalk Service souhaité toobackup.</span><span class="sxs-lookup"><span data-stu-id="607e5-135">In hello Azure classic portal, select **BizTalk Services**, and then select hello BizTalk Service you want toobackup.</span></span>
2. <span data-ttu-id="607e5-136">Bonjour **tableau de bord** onglet, sélectionnez **sauvegarder** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="607e5-136">In hello **Dashboard** tab, select **Back up** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="607e5-137">Entrez un nom de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="607e5-137">Enter a backup name.</span></span> <span data-ttu-id="607e5-138">Par exemple, entrez *monServiceBizTalk*BU*Date*.</span><span class="sxs-lookup"><span data-stu-id="607e5-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="607e5-139">Choisissez un compte de stockage d’objets blob et de la sauvegarde de hello sélectionnez coche toostart hello.</span><span class="sxs-lookup"><span data-stu-id="607e5-139">Choose a blob storage account and select hello checkmark toostart hello backup.</span></span>

<span data-ttu-id="607e5-140">Une fois la sauvegarde de hello terminée, un conteneur avec le nom de la sauvegarde hello que vous entrez est créé dans le compte de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="607e5-140">Once hello backup completes, a container with hello backup name you enter is created in hello storage account.</span></span> <span data-ttu-id="607e5-141">Ce conteneur comprend la configuration de sauvegarde de votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="607e5-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="607e5-142"><a name="backupschedule"></a>Planification d'une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="607e5-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="607e5-143">Bonjour portail Azure classic, sélectionnez **BizTalk Services**, sélectionnez hello BizTalk Service nom tooschedule hello sauvegarde, puis sélectionnez hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="607e5-143">In hello Azure classic portal, select **BizTalk Services**, select hello BizTalk Service name you want tooschedule hello backup, and then select hello **Configure** tab.</span></span>
2. <span data-ttu-id="607e5-144">Ensemble hello **état de la sauvegarde** trop**automatique**.</span><span class="sxs-lookup"><span data-stu-id="607e5-144">Set hello **Backup Status** too**Automatic**.</span></span> 
3. <span data-ttu-id="607e5-145">Sélectionnez hello **compte de stockage** toostore hello sauvegarde, entrez hello **fréquence** toocreate hello sauvegardes et la durée pendant laquelle tookeep hello (**jours de rétention**) :</span><span class="sxs-lookup"><span data-stu-id="607e5-145">Select hello **Storage Account** toostore hello backup, enter hello **Frequency** toocreate hello backups, and how long tookeep hello backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="607e5-146">**Remarques**</span><span class="sxs-lookup"><span data-stu-id="607e5-146">**Notes**</span></span>     
   
   * <span data-ttu-id="607e5-147">Dans **jours de rétention**, période de rétention hello doit être supérieure à la fréquence de sauvegarde hello.</span><span class="sxs-lookup"><span data-stu-id="607e5-147">In **Retention Days**, hello retention period must be greater than hello backup frequency.</span></span>
   * <span data-ttu-id="607e5-148">Sélectionnez **conserver toujours au moins une sauvegarde**, même si elle est au-delà de la période de rétention hello.</span><span class="sxs-lookup"><span data-stu-id="607e5-148">Select **Always keep at least one backup**, even if it is past hello retention period.</span></span>
4. <span data-ttu-id="607e5-149">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="607e5-149">Select **Save**.</span></span>

<span data-ttu-id="607e5-150">Lorsqu’une tâche de sauvegarde planifiée s’exécute, il crée un conteneur (données de sauvegarde toostore) dans le compte de stockage hello que vous avez entré.</span><span class="sxs-lookup"><span data-stu-id="607e5-150">When a scheduled backup job runs, it creates a container (toostore backup data) in hello storage account you entered.</span></span> <span data-ttu-id="607e5-151">nom Hello du conteneur de hello est nommé *BizTalk Service nom-date-heure*.</span><span class="sxs-lookup"><span data-stu-id="607e5-151">hello name of hello container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="607e5-152">Si hello tableau de bord de BizTalk Service affiche un **n’a pas pu** état :</span><span class="sxs-lookup"><span data-stu-id="607e5-152">If hello BizTalk Service dashboard shows a **Failed** status:</span></span>

![Statut de la dernière sauvegarde planifiée][BackupStatus] 

<span data-ttu-id="607e5-154">Hello ouvre hello gestion des Services de journaux des opérations toohelp résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="607e5-154">hello link opens hello Management Services Operation Logs toohelp troubleshoot.</span></span> <span data-ttu-id="607e5-155">Consultez [BizTalk Services : résolution des problèmes à l'aide des journaux des opérations](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="607e5-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="607e5-156">Restauration</span><span class="sxs-lookup"><span data-stu-id="607e5-156">Restore</span></span>
<span data-ttu-id="607e5-157">Vous pouvez restaurer les sauvegardes à partir de hello portail Azure classic ou de hello [restaurer API REST du Service BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="607e5-157">You can restore backups from hello Azure classic portal or from hello [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="607e5-158">Cette section répertorie les toorestore d’étapes hello à l’aide du portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="607e5-158">This section lists hello steps toorestore using hello classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="607e5-159">Avant de restaurer une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="607e5-159">Before restoring a backup</span></span>
* <span data-ttu-id="607e5-160">De nouveaux magasins de suivi, d'archivage et de surveillance peuvent être spécifiés lors de la restauration d'un service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="607e5-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="607e5-161">Hello les mêmes données de Runtime de EDI sont restaurées.</span><span class="sxs-lookup"><span data-stu-id="607e5-161">hello same EDI Runtime data is restored.</span></span> <span data-ttu-id="607e5-162">sauvegarde de EDI Runtime Hello stocke des numéros de contrôle hello.</span><span class="sxs-lookup"><span data-stu-id="607e5-162">hello EDI Runtime backup stores hello control numbers.</span></span> <span data-ttu-id="607e5-163">numéros de contrôle Hello restauré sont séquentiels hello à partir de la sauvegarde de hello.</span><span class="sxs-lookup"><span data-stu-id="607e5-163">hello restored control numbers are in sequence from hello time of hello backup.</span></span> <span data-ttu-id="607e5-164">Si les messages sont traités après la dernière sauvegarde de hello, la restauration ce contenu de la sauvegarde peut entraîner des numéros de contrôle en double.</span><span class="sxs-lookup"><span data-stu-id="607e5-164">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="607e5-165">Restauration d'une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="607e5-165">Restore a backup</span></span>
1. <span data-ttu-id="607e5-166">Bonjour portail Azure classic, sélectionnez **nouveau** > **des Services d’application** > **BizTalk Service** > **restaurer** :</span><span class="sxs-lookup"><span data-stu-id="607e5-166">In hello Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Restauration d'une sauvegarde][Restore]
2. <span data-ttu-id="607e5-168">Dans **sauvegarde URL**, sélectionnez l’icône de dossier hello et développez le compte de stockage Azure hello que magasins hello sauvegarde de configuration de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="607e5-168">In **Backup URL**, select hello folder icon and expand hello Azure storage account that stores hello BizTalk Service configuration backup.</span></span> <span data-ttu-id="607e5-169">Développez le conteneur de hello et dans le volet droit de hello, sélectionnez hello correspondant sauvegarder le fichier .txt.</span><span class="sxs-lookup"><span data-stu-id="607e5-169">Expand hello container and in hello right pane, select hello corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="607e5-170">Sélectionnez **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="607e5-170">Select **Open**.</span></span>
3. <span data-ttu-id="607e5-171">Sur hello **restaurer le BizTalk Service** , entrez un **nom du Service BizTalk** et vérifiez hello **URL de domaine**, **édition**et **Région** pour hello restauré BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="607e5-171">On hello **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify hello **Domain URL**, **Edition**, and **Region** for hello restored BizTalk Service.</span></span> <span data-ttu-id="607e5-172">**Créer une nouvelle instance de la base de données SQL** pour hello de base de données de suivi :</span><span class="sxs-lookup"><span data-stu-id="607e5-172">**Create a new SQL database instance** for hello tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="607e5-173">Sélectionnez la flèche suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="607e5-173">Select hello next arrow.</span></span>
4. <span data-ttu-id="607e5-174">Vérifiez le nom hello de base de données SQL hello, entrez hello de serveur physique où la base de données SQL hello doit être créé et un nom d’utilisateur/mot de passe pour ce serveur.</span><span class="sxs-lookup"><span data-stu-id="607e5-174">Verify hello name of hello SQL database, enter hello physical server where hello SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="607e5-175">Si vous souhaitez l’édition de base de données SQL tooconfigure hello, de taille et d’autres propriétés, sélectionnez **configurer des paramètres avancés de base de données**.</span><span class="sxs-lookup"><span data-stu-id="607e5-175">If you want tooconfigure hello SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="607e5-176">Sélectionnez la flèche suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="607e5-176">Select hello next arrow.</span></span>

1. <span data-ttu-id="607e5-177">Créer un nouveau compte de stockage, ou entrez un compte de stockage existant pour hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="607e5-177">Create a new storage account or enter an existing storage account for hello BizTalk Service.</span></span>
2. <span data-ttu-id="607e5-178">Sélectionnez hello coche toostart hello restaurer.</span><span class="sxs-lookup"><span data-stu-id="607e5-178">Select hello checkmark toostart hello restore.</span></span>

<span data-ttu-id="607e5-179">Une fois la restauration de hello terminée avec succès, un BizTalk Service est répertorié dans l’état suspendu sur la page des Services BizTalk hello Bonjour portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="607e5-179">Once hello restoration successfully completes, a new BizTalk Service is listed in a suspended state on hello BizTalk Services page in hello Azure classic portal.</span></span>

### <span data-ttu-id="607e5-180"><a name="postrestore"></a>Après avoir restauré une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="607e5-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="607e5-181">Hello BizTalk Service est toujours restauré dans un **Suspended** état.</span><span class="sxs-lookup"><span data-stu-id="607e5-181">hello BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="607e5-182">Dans cet état, vous pouvez modifier n’importe quel configuration avant que le nouvel environnement de hello est fonctionnelle, y compris :</span><span class="sxs-lookup"><span data-stu-id="607e5-182">In this state, you can make any configuration changes before hello new environment is functional, including:</span></span>

* <span data-ttu-id="607e5-183">Si vous avez créé des applications de BizTalk Service à l’aide de hello Azure BizTalk Services SDK, vous devrez peut-être les informations d’identification de tootooupdate hello Access Control (ACS) dans ces toowork d’applications avec l’environnement de hello restaurée.</span><span class="sxs-lookup"><span data-stu-id="607e5-183">If you created BizTalk Service applications using hello Azure BizTalk Services SDK, you may need tootooupdate hello Access Control (ACS) credentials in those applications toowork with hello restored environment.</span></span>
* <span data-ttu-id="607e5-184">Vous restaurez un tooreplicate de BizTalk Service un environnement de BizTalk Service existant.</span><span class="sxs-lookup"><span data-stu-id="607e5-184">You restore a BizTalk Service tooreplicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="607e5-185">Dans ce cas, s’il existe des accords configurés dans le portail BizTalk Services d’origine hello qui utilisent un dossier source FTP, vous devrez peut-être tooupdate les accords de hello en hello récemment restauré environnement toouse un serveur FTP source différente.</span><span class="sxs-lookup"><span data-stu-id="607e5-185">In this situation, if there are agreements configured in hello original BizTalk Services portal that use a source FTP folder, you may need tooupdate hello agreements in hello newly restored environment toouse a different source FTP folder.</span></span> <span data-ttu-id="607e5-186">Dans le cas contraire, il peut y avoir deux contrats différents lors de la tentative toopull hello même message.</span><span class="sxs-lookup"><span data-stu-id="607e5-186">Otherwise, there may be two different agreements trying toopull hello same message.</span></span>
* <span data-ttu-id="607e5-187">Si vous avez restauré toohave plusieurs environnements de BizTalk Service, assurez-vous que vous ciblez l’environnement approprié de hello dans les applications Visual Studio hello, les applets de commande PowerShell, les API REST ou les API OM de gestion des partenaires commerciaux.</span><span class="sxs-lookup"><span data-stu-id="607e5-187">If you restored toohave multiple BizTalk Service environments, make sure you target hello correct environment in hello Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="607e5-188">Il est conseillé tooconfigure automatisée sauvegardes dans l’environnement du Service BizTalk hello qui vient d’être restaurée.</span><span class="sxs-lookup"><span data-stu-id="607e5-188">It's a good practice tooconfigure automated backups on hello newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="607e5-189">toostart hello BizTalk Service Bonjour portail Azure classic, sélectionnez hello restauré BizTalk Service et sélectionnez **reprise** dans la barre des tâches hello.</span><span class="sxs-lookup"><span data-stu-id="607e5-189">toostart hello BizTalk Service in hello Azure classic portal, select hello restored BizTalk Service and select **Resume** in hello task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="607e5-190">Éléments sauvegardés</span><span class="sxs-lookup"><span data-stu-id="607e5-190">What gets backed up</span></span>
<span data-ttu-id="607e5-191">Lors de la création d’une sauvegarde, hello éléments suivants sont sauvegardés :</span><span class="sxs-lookup"><span data-stu-id="607e5-191">When a backup is created, hello following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="607e5-192">Éléments sauvegardés</span><span class="sxs-lookup"><span data-stu-id="607e5-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="607e5-193">
 <strong>Portail Azure BizTalk Services</strong></span><span class="sxs-lookup"><span data-stu-id="607e5-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="607e5-194">Configuration et exécution</span><span class="sxs-lookup"><span data-stu-id="607e5-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="607e5-195">Détails du partenaire et du profil</span><span class="sxs-lookup"><span data-stu-id="607e5-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="607e5-196">Contrats partenaires</span><span class="sxs-lookup"><span data-stu-id="607e5-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="607e5-197">Assemblys personnalisés déployés</span><span class="sxs-lookup"><span data-stu-id="607e5-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="607e5-198">Ponts déployés</span><span class="sxs-lookup"><span data-stu-id="607e5-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="607e5-199">Certificats</span><span class="sxs-lookup"><span data-stu-id="607e5-199">Certificates</span></span></li>
<li><span data-ttu-id="607e5-200">Transformations déployées</span><span class="sxs-lookup"><span data-stu-id="607e5-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="607e5-201">Pipelines</span><span class="sxs-lookup"><span data-stu-id="607e5-201">Pipelines</span></span></li>
<li><span data-ttu-id="607e5-202">Modèles créés et enregistrés dans hello portail BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="607e5-202">Templates created and saved in hello BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="607e5-203">Mappages X12 ST01 et GS01</span><span class="sxs-lookup"><span data-stu-id="607e5-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="607e5-204">Numéros de contrôle (EDI)</span><span class="sxs-lookup"><span data-stu-id="607e5-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="607e5-205">Valeurs MIC des messages AS2</span><span class="sxs-lookup"><span data-stu-id="607e5-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="607e5-206">
 <strong>Azure BizTalk Service</strong></span><span class="sxs-lookup"><span data-stu-id="607e5-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="607e5-207">Certificat SSL</span><span class="sxs-lookup"><span data-stu-id="607e5-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="607e5-208">Données du certificat SSL</span><span class="sxs-lookup"><span data-stu-id="607e5-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="607e5-209">Mot de passe du certificat SSL</span><span class="sxs-lookup"><span data-stu-id="607e5-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="607e5-210">Paramètres du service BizTalk</span><span class="sxs-lookup"><span data-stu-id="607e5-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="607e5-211">Nombre d'unités mises à l'échelle</span><span class="sxs-lookup"><span data-stu-id="607e5-211">Scale unit count</span></span></li>
<li><span data-ttu-id="607e5-212">Édition</span><span class="sxs-lookup"><span data-stu-id="607e5-212">Edition</span></span></li>
<li><span data-ttu-id="607e5-213">Version du produit</span><span class="sxs-lookup"><span data-stu-id="607e5-213">Product Version</span></span></li>
<li><span data-ttu-id="607e5-214">Région/centre de données</span><span class="sxs-lookup"><span data-stu-id="607e5-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="607e5-215">Espace de noms et clé Access Control Service (ACS)</span><span class="sxs-lookup"><span data-stu-id="607e5-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="607e5-216">Chaîne de connexion à la base de données de suivi</span><span class="sxs-lookup"><span data-stu-id="607e5-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="607e5-217">Chaîne de connexion au compte de stockage d'archive</span><span class="sxs-lookup"><span data-stu-id="607e5-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="607e5-218">Chaîne de connexion au compte de stockage de surveillance</span><span class="sxs-lookup"><span data-stu-id="607e5-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="607e5-219">
 <strong>Autres éléments</strong></span><span class="sxs-lookup"><span data-stu-id="607e5-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="607e5-220">Base de données des suivis</span><span class="sxs-lookup"><span data-stu-id="607e5-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="607e5-221">Lorsque hello BizTalk Service est créé, les détails de base de données de suivi hello sont entrés, notamment hello serveur de base de données SQL Azure et le nom de base de données de suivi hello.</span><span class="sxs-lookup"><span data-stu-id="607e5-221">When hello BizTalk Service is created, hello Tracking Database details are entered, including hello Azure SQL Database Server and hello Tracking Database name.</span></span> <span data-ttu-id="607e5-222">Hello de base de données de suivi n’est pas automatiquement sauvegardée.</span><span class="sxs-lookup"><span data-stu-id="607e5-222">hello Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="607e5-223">
<strong>Important</strong></span><span class="sxs-lookup"><span data-stu-id="607e5-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="607e5-224">Si hello suivi de la base de données est supprimée et hello des besoins de base de données récupérées, une sauvegarde précédente doit exister.</span><span class="sxs-lookup"><span data-stu-id="607e5-224">If hello Tracking Database is deleted and hello database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="607e5-225">Si une sauvegarde n’existe pas, hello suivi de la base de données et ses données ne sont pas récupérables.</span><span class="sxs-lookup"><span data-stu-id="607e5-225">If a backup does not exist, hello Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="607e5-226">Dans ce cas, créez une nouvelle base de données de suivi avec hello même nom de base de données.</span><span class="sxs-lookup"><span data-stu-id="607e5-226">In this situation, create a new Tracking Database with hello same database name.</span></span> <span data-ttu-id="607e5-227">La géo-réplication est recommandée.</span><span class="sxs-lookup"><span data-stu-id="607e5-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="607e5-228">Suivant</span><span class="sxs-lookup"><span data-stu-id="607e5-228">Next</span></span>
<span data-ttu-id="607e5-229">toocreate Azure BizTalk Services dans hello Azure classic, accédez trop[BizTalk Services : portail classique de configuration à l’aide Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="607e5-229">toocreate Azure BizTalk Services in hello Azure classic portal, go too[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="607e5-230">toostart création d’applications, accédez trop[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="607e5-230">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="607e5-231">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="607e5-231">See Also</span></span>
* [<span data-ttu-id="607e5-232">Sauvegarde d'un service BizTalk</span><span class="sxs-lookup"><span data-stu-id="607e5-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="607e5-233">Restauration d'un service BizTalk depuis une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="607e5-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="607e5-234">Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="607e5-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="607e5-235">BizTalk Services : approvisionnement à l’aide du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="607e5-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="607e5-236">Tableau comparatif des états d'approvisionnement BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="607e5-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="607e5-237">Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="607e5-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="607e5-238">Limitation dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="607e5-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="607e5-239">Nom et clé de l'émetteur dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="607e5-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="607e5-240">Comment puis-je démarrer à l’aide de hello SDK des Services BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="607e5-240">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png

