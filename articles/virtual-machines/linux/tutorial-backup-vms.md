---
title: Sauvegarder des machines virtuelles Linux Azure | Microsoft Docs
description: "Protégez vos machines virtuelles Linux en les sauvegardant à l’aide d’Azure Backup."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="540b1-103">Sauvegarder des machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="540b1-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="540b1-104">Vous pouvez protéger vos données en effectuant des sauvegardes à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="540b1-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="540b1-105">Azure Backup crée des points de récupération stockés dans des coffres de récupération géoredondants.</span><span class="sxs-lookup"><span data-stu-id="540b1-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="540b1-106">Lorsque vous restaurez à partir d’un point de récupération, vous pouvez restaurer hello toute machine virtuelle ou des fichiers spécifiques.</span><span class="sxs-lookup"><span data-stu-id="540b1-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="540b1-107">Cet article explique comment toorestore un seul fichier tooa nginx en cours d’exécution de Linux VM.</span><span class="sxs-lookup"><span data-stu-id="540b1-107">This article explains how toorestore a single file tooa Linux VM running nginx.</span></span> <span data-ttu-id="540b1-108">Si vous n’avez pas encore un toouse de machine virtuelle, vous pouvez en créer un à l’aide de hello [Linux quickstart](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="540b1-108">If you don't already have a VM toouse, you can create one using hello [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="540b1-109">Ce didacticiel vous explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="540b1-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="540b1-110">Créer une sauvegarde de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="540b1-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="540b1-111">Planifier une sauvegarde quotidienne</span><span class="sxs-lookup"><span data-stu-id="540b1-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="540b1-112">Restaurer un fichier à partir d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="540b1-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="540b1-113">Présentation de la sauvegarde</span><span class="sxs-lookup"><span data-stu-id="540b1-113">Backup overview</span></span>

<span data-ttu-id="540b1-114">Hello service Azure Backup lorsqu’une sauvegarde, il déclenche hello extension de sauvegarde tootake un instantané de point-à-temps.</span><span class="sxs-lookup"><span data-stu-id="540b1-114">When hello Azure Backup service initiates a backup, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="540b1-115">Hello service Azure Backup utilise hello _VMSnapshotLinux_ extension dans Linux.</span><span class="sxs-lookup"><span data-stu-id="540b1-115">hello Azure Backup service uses hello _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="540b1-116">extension de Hello est installée au cours de la première sauvegarde de machine virtuelle hello si hello machine virtuelle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="540b1-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="540b1-117">Si hello machine virtuelle ne fonctionne pas, hello service de sauvegarde prend un instantané de hello stockage sous-jacent (dans la mesure où aucune écriture de l’application se produire lors de la machine virtuelle est arrêtée de hello).</span><span class="sxs-lookup"><span data-stu-id="540b1-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="540b1-118">Par défaut, Azure Backup prend une sauvegarde cohérente de système de fichiers pour Linux VM, mais il peut être configuré tootake [sauvegarde cohérente d’application à l’aide du script avant et après script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span><span class="sxs-lookup"><span data-stu-id="540b1-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured tootake [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="540b1-119">Une fois que hello service Azure Backup prend un instantané de hello, données de hello sont transférées toohello coffre.</span><span class="sxs-lookup"><span data-stu-id="540b1-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="540b1-120">l’efficacité toomaximize, hello service identifie et transfère uniquement les blocs de hello de données qui ont été modifiés depuis la sauvegarde précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="540b1-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="540b1-121">Lorsque le transfert de données hello est terminé, les instantanés hello sont supprimé et un point de récupération est créé.</span><span class="sxs-lookup"><span data-stu-id="540b1-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="540b1-122">Création d'une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="540b1-122">Create a backup</span></span>
<span data-ttu-id="540b1-123">Créer une simple planifiée quotidienne sauvegarde tooa coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="540b1-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="540b1-124">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="540b1-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="540b1-125">Dans le menu hello hello gauche, sélectionnez **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="540b1-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="540b1-126">À partir de la liste de hello, sélectionnez un tooback de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="540b1-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="540b1-127">Dans Panneau de machine virtuelle hello, Bonjour **paramètres** , cliquez sur **sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="540b1-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="540b1-128">Hello **Active la sauvegarde** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="540b1-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="540b1-129">Dans **de coffre Recovery Services**, cliquez sur **nouvel** et fournir le nom hello pour le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="540b1-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="540b1-130">Un nouvel archivage est créé dans hello même groupe de ressources et l’emplacement en tant que machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="540b1-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="540b1-131">Cliquez sur **Stratégie de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="540b1-131">Click **Backup policy**.</span></span> <span data-ttu-id="540b1-132">Pour cet exemple, conservez les valeurs par défaut hello et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="540b1-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="540b1-133">Sur hello **Active la sauvegarde** panneau, cliquez sur **activez la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="540b1-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="540b1-134">Cette opération crée une sauvegarde quotidienne selon une planification par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="540b1-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="540b1-135">toocreate un point de récupération initial sur hello **sauvegarde** cliquez sur le panneau **sauvegarder maintenant**.</span><span class="sxs-lookup"><span data-stu-id="540b1-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="540b1-136">Sur hello **sauvegarde maintenant** panneau, cliquez sur icône du calendrier hello, utilisez Bonjour calendrier contrôle tooselect Bonjour dernier jour de ce point de récupération est conservé, puis cliquez sur **sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="540b1-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="540b1-137">Bonjour **sauvegarde** panneau pour votre machine virtuelle, vous verrez nombre hello de points de récupération qui sont terminées.</span><span class="sxs-lookup"><span data-stu-id="540b1-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Points de récupération](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="540b1-139">première sauvegarde de Hello prend environ 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="540b1-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="540b1-140">Continuer toohello la partie suivante de ce didacticiel, une fois la sauvegarde terminée.</span><span class="sxs-lookup"><span data-stu-id="540b1-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="540b1-141">Restaurer un fichier</span><span class="sxs-lookup"><span data-stu-id="540b1-141">Restore a file</span></span>

<span data-ttu-id="540b1-142">Si vous supprimez ou rendre le fichier tooa des modifications, vous pouvez utiliser le fichier de récupération de fichier toorecover hello votre coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="540b1-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="540b1-143">Récupération de fichiers utilise un script qui s’exécute sur hello machine virtuelle, point de récupération toomount hello en tant que lecteur local.</span><span class="sxs-lookup"><span data-stu-id="540b1-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="540b1-144">Ces lecteurs restera montés pendant 12 heures, afin que vous pouvez copier les fichiers de point de récupération hello et restaurez-les toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="540b1-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="540b1-145">Dans cet exemple, nous montrons comment toorecover hello par défaut nginx page web /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="540b1-145">In this example, we show how toorecover hello default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="540b1-146">Hello une adresse IP publique de votre machine virtuelle dans cet exemple est *13.69.75.209*.</span><span class="sxs-lookup"><span data-stu-id="540b1-146">hello public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="540b1-147">Vous pouvez trouver l’adresse IP de hello de votre machine virtuelle à l’aide :</span><span class="sxs-lookup"><span data-stu-id="540b1-147">You can find hello IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="540b1-148">Sur votre ordinateur local, ouvrez un navigateur et tapez dans hello adresse IP publique de votre page web de machine virtuelle toosee hello par défaut nginx.</span><span class="sxs-lookup"><span data-stu-id="540b1-148">On your local computer, open a browser and type in hello public IP address of your VM toosee hello default nginx web page.</span></span>

    ![Page web nginx par défaut](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="540b1-150">Connectez-vous avec SSH à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="540b1-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="540b1-151">Supprimez /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="540b1-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="540b1-152">Sur votre ordinateur local, actualisez le navigateur de hello en appuyant sur CTRL + F5 toosee qui nginx page par défaut a disparu.</span><span class="sxs-lookup"><span data-stu-id="540b1-152">On your local computer, refresh hello browser by hitting CTRL + F5 toosee that default nginx page is gone.</span></span>

    ![Page web nginx par défaut](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="540b1-154">Sur votre ordinateur local, connectez-vous en toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="540b1-154">On your local computer, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="540b1-155">Dans le menu hello hello gauche, sélectionnez **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="540b1-155">In hello menu on hello left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="540b1-156">Dans la liste hello, sélectionnez hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="540b1-156">From hello list, select hello VM.</span></span>
8. <span data-ttu-id="540b1-157">Dans Panneau de machine virtuelle hello, Bonjour **paramètres** , cliquez sur **sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="540b1-157">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="540b1-158">Hello **sauvegarde** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="540b1-158">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="540b1-159">Dans le menu hello haut hello du Panneau de hello, sélectionnez **récupération de fichier**.</span><span class="sxs-lookup"><span data-stu-id="540b1-159">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="540b1-160">Hello **récupération de fichier** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="540b1-160">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="540b1-161">Dans **étape 1 : sélectionnez le point de récupération**, sélectionnez un point de récupération à partir de hello de liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="540b1-161">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="540b1-162">Dans **étape 2 : télécharger le script toobrowse et récupérer les fichiers**, cliquez sur hello **télécharger le fichier exécutable** bouton.</span><span class="sxs-lookup"><span data-stu-id="540b1-162">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="540b1-163">Enregistrer l’ordinateur local du tooyour hello fichier téléchargé.</span><span class="sxs-lookup"><span data-stu-id="540b1-163">Save hello downloaded file tooyour local computer.</span></span>
7. <span data-ttu-id="540b1-164">Cliquez sur **télécharger le script** fichier de script hello toodownload localement.</span><span class="sxs-lookup"><span data-stu-id="540b1-164">Click **Download script** toodownload hello script file locally.</span></span>
8. <span data-ttu-id="540b1-165">Ouvrez un Bonjour Bash invite et le type suivant, en remplaçant *Linux_myVM_05-05-2017.sh* avec hello corriger le chemin d’accès et nom de fichier de script hello que vous avez téléchargé, *azureuser* UserName hello pour hello machine virtuelle et *13.69.75.209* avec l’adresse IP publique de hello pour votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="540b1-165">Open a Bash prompt and type hello following, replacing *Linux_myVM_05-05-2017.sh* with hello correct path and filename for hello script that you downloaded, *azureuser* with hello username for hello VM and *13.69.75.209* with hello public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="540b1-166">Sur votre ordinateur local, ouvrez un toohello de connexion SSH machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="540b1-166">On your local computer, open an SSH connection toohello VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="540b1-167">Sur votre machine virtuelle, ajoutez d’exécuter le fichier de script toohello autorisations.</span><span class="sxs-lookup"><span data-stu-id="540b1-167">On your VM, add execute permissions toohello script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="540b1-168">Sur votre machine virtuelle, exécutez le point de récupération hello hello script toomount comme un système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="540b1-168">On your VM, run hello script toomount hello recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="540b1-169">Hello de sortie à partir de l’offre de script hello que Hello de chemin d’accès pour le point de montage hello.</span><span class="sxs-lookup"><span data-stu-id="540b1-169">hello output from hello script gives you hello path for hello mount point.</span></span> <span data-ttu-id="540b1-170">sortie de Hello ressemble toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="540b1-170">hello output looks similar toothis:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. <span data-ttu-id="540b1-171">Sur votre machine virtuelle, copiez la page web de hello nginx par défaut à partir de toowhere arrière du point de montage hello vous avez supprimé les fichier hello.</span><span class="sxs-lookup"><span data-stu-id="540b1-171">On your VM, copy hello nginx default web page from hello mount point back toowhere you deleted hello file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="540b1-172">Sur votre ordinateur local, ouvrez l’onglet de navigateur hello où vous êtes connecté adresse toohello de hello VM écran hello nginx par défaut de la page.</span><span class="sxs-lookup"><span data-stu-id="540b1-172">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello nginx default page.</span></span> <span data-ttu-id="540b1-173">Appuyez sur CTRL + F5 page du navigateur toorefresh hello.</span><span class="sxs-lookup"><span data-stu-id="540b1-173">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="540b1-174">Vous devez maintenant voir que hello page par défaut fonctionne à nouveau.</span><span class="sxs-lookup"><span data-stu-id="540b1-174">You should now see that hello default page is working again.</span></span>

    ![Page web nginx par défaut](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="540b1-176">Sur votre ordinateur local, revenir en arrière toohello onglet du navigateur pour hello portail Azure et dans **étape 3 : démontage de disques de hello après la récupération** cliquez sur hello **démontage de disques** bouton.</span><span class="sxs-lookup"><span data-stu-id="540b1-176">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="540b1-177">Si vous oubliez toodo cette étape, point de montage toohello hello connexion est automatiquement fermée après 12 heures.</span><span class="sxs-lookup"><span data-stu-id="540b1-177">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="540b1-178">Après les 12 heures, vous devez toodownload une nouvelle toocreate de script un nouveau point de montage.</span><span class="sxs-lookup"><span data-stu-id="540b1-178">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="540b1-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="540b1-179">Next steps</span></span>

<span data-ttu-id="540b1-180">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="540b1-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="540b1-181">Créer une sauvegarde de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="540b1-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="540b1-182">Planifier une sauvegarde quotidienne</span><span class="sxs-lookup"><span data-stu-id="540b1-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="540b1-183">Restaurer un fichier à partir d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="540b1-183">Restore a file from a backup</span></span>

<span data-ttu-id="540b1-184">Avance toohello toolearn de didacticiel suivant sur l’analyse des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="540b1-184">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="540b1-185">Surveiller les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="540b1-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

