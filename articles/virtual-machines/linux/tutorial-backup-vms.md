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
ms.openlocfilehash: d0cbf7883a8737bcb10e9dd251c9792a12993f77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="f3804-103">Sauvegarder des machines virtuelles Linux dans Azure</span><span class="sxs-lookup"><span data-stu-id="f3804-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="f3804-104">Vous pouvez protéger vos données en effectuant des sauvegardes à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="f3804-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="f3804-105">Azure Backup crée des points de récupération stockés dans des coffres de récupération géoredondants.</span><span class="sxs-lookup"><span data-stu-id="f3804-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="f3804-106">Lorsque vous effectuez une restauration à partir d’un point de récupération, vous pouvez restaurer la machine virtuelle entière ou seulement des fichiers spécifiques.</span><span class="sxs-lookup"><span data-stu-id="f3804-106">When you restore from a recovery point, you can restore the whole VM or just specific files.</span></span> <span data-ttu-id="f3804-107">Cet article explique comment restaurer un fichier unique sur une machine virtuelle Linux exécutant nginx.</span><span class="sxs-lookup"><span data-stu-id="f3804-107">This article explains how to restore a single file to a Linux VM running nginx.</span></span> <span data-ttu-id="f3804-108">Si vous ne disposez d’aucune machine virtuelle, vous pouvez en créer une à l’aide du [démarrage rapide Linux](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f3804-108">If you don't already have a VM to use, you can create one using the [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="f3804-109">Ce didacticiel vous montre comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f3804-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f3804-110">Créer une sauvegarde de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f3804-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="f3804-111">Planifier une sauvegarde quotidienne</span><span class="sxs-lookup"><span data-stu-id="f3804-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="f3804-112">Restaurer un fichier à partir d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="f3804-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="f3804-113">Présentation de la sauvegarde</span><span class="sxs-lookup"><span data-stu-id="f3804-113">Backup overview</span></span>

<span data-ttu-id="f3804-114">Lorsque le service Azure Backup lance une sauvegarde, il déclenche l’extension de sauvegarde pour prendre un instantané à un moment donné.</span><span class="sxs-lookup"><span data-stu-id="f3804-114">When the Azure Backup service initiates a backup, it triggers the backup extension to take a point-in-time snapshot.</span></span> <span data-ttu-id="f3804-115">Le service Azure Backup utilise l’extension _VMSnapshotLinux_ dans Linux.</span><span class="sxs-lookup"><span data-stu-id="f3804-115">The Azure Backup service uses the _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="f3804-116">L’extension est installée lors de la première sauvegarde de machine virtuelle si cette machine virtuelle est exécutée.</span><span class="sxs-lookup"><span data-stu-id="f3804-116">The extension is installed during the first VM backup if the VM is running.</span></span> <span data-ttu-id="f3804-117">Si la machine virtuelle n’est pas en cours d’exécution, le service Sauvegarde prend un instantané du stockage sous-jacent (car aucune écriture de l’application n’a lieu pendant l’arrêt de la machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="f3804-117">If the VM is not running, the Backup service takes a snapshot of the underlying storage (since no application writes occur while the VM is stopped).</span></span>

<span data-ttu-id="f3804-118">Par défaut, le service Azure Backup effectue une sauvegarde cohérente avec le système de fichiers pour la machine virtuelle Linux, bien qu’il puisse être configuré pour effectuer une [sauvegarde cohérente avec les applications en utilisant des infrastructures pré-script et post-script](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span><span class="sxs-lookup"><span data-stu-id="f3804-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured to take [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="f3804-119">Après que le service Sauvegarde Azure a pris l’instantané, les données sont transférées vers le coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="f3804-119">Once the Azure Backup service takes the snapshot, the data is transferred to the vault.</span></span> <span data-ttu-id="f3804-120">Pour optimiser l’efficacité, le service identifie et transfère uniquement les blocs de données qui ont été modifiés depuis la sauvegarde précédente.</span><span class="sxs-lookup"><span data-stu-id="f3804-120">To maximize efficiency, the service identifies and transfers only the blocks of data that have changed since the previous backup.</span></span>

<span data-ttu-id="f3804-121">Une fois le transfert de données terminé, l’instantané est supprimé et un point de récupération est créé.</span><span class="sxs-lookup"><span data-stu-id="f3804-121">When the data transfer is complete, the snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="f3804-122">Création d'une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="f3804-122">Create a backup</span></span>
<span data-ttu-id="f3804-123">Créez une simple sauvegarde quotidienne planifiée dans un coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="f3804-123">Create a simple scheduled daily backup to a Recovery Services Vault.</span></span> 

1. <span data-ttu-id="f3804-124">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f3804-124">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="f3804-125">Dans le menu de gauche, sélectionnez **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="f3804-125">In the menu on the left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="f3804-126">Dans la liste, sélectionnez la machine virtuelle que vous souhaitez sauvegarder.</span><span class="sxs-lookup"><span data-stu-id="f3804-126">From the list, select a VM to back up.</span></span>
4. <span data-ttu-id="f3804-127">Dans le panneau de la machine virtuelle, au niveau de la section **Paramètres**, cliquez sur **Sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="f3804-127">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="f3804-128">Le panneau **Activer la sauvegarde** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="f3804-128">The **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="f3804-129">Dans **Coffre Recovery Services**, cliquez sur **Créer** et fournissez le nom du nouveau coffre.</span><span class="sxs-lookup"><span data-stu-id="f3804-129">In **Recovery Services vault**, click **Create new** and provide the name for the new vault.</span></span> <span data-ttu-id="f3804-130">Un coffre est créé dans le même groupe de ressources et au même emplacement que la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f3804-130">A new vault is created in the same Resource Group and location as the virtual machine.</span></span>
6. <span data-ttu-id="f3804-131">Cliquez sur **Stratégie de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="f3804-131">Click **Backup policy**.</span></span> <span data-ttu-id="f3804-132">Pour cet exemple, conservez les valeurs par défaut et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f3804-132">For this example, keep the defaults and click **OK**.</span></span>
7. <span data-ttu-id="f3804-133">Dans le panneau **Activer la sauvegarde**, cliquez sur **Activer la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="f3804-133">On the **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="f3804-134">Cette opération crée une sauvegarde quotidienne selon la planification par défaut.</span><span class="sxs-lookup"><span data-stu-id="f3804-134">This creates a daily backup based on the default schedule.</span></span>
10. <span data-ttu-id="f3804-135">Pour créer un point de récupération initial, dans le panneau **Sauvegarde**, cliquez sur **Sauvegarder maintenant**.</span><span class="sxs-lookup"><span data-stu-id="f3804-135">To create an initial recovery point, on the **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="f3804-136">Dans le panneau **Sauvegarder maintenant**, cliquez sur l’icône de calendrier. Utilisez le contrôle de calendrier pour sélectionner le dernier jour de conservation de ce point de récupération, puis cliquez sur **Sauvegarder**.</span><span class="sxs-lookup"><span data-stu-id="f3804-136">On the **Backup Now** blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="f3804-137">Le panneau **Sauvegarde** de votre machine virtuelle affiche le nombre de points de récupération terminés.</span><span class="sxs-lookup"><span data-stu-id="f3804-137">In the **Backup** blade for your VM, you will see the number of recovery points that are complete.</span></span>

    ![Points de récupération](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="f3804-139">La première sauvegarde prend environ 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="f3804-139">The first backup takes about 20 minutes.</span></span> <span data-ttu-id="f3804-140">Une fois la sauvegarde terminée, passez à l’étape suivante de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f3804-140">Proceed to the next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="f3804-141">Restaurer un fichier</span><span class="sxs-lookup"><span data-stu-id="f3804-141">Restore a file</span></span>

<span data-ttu-id="f3804-142">Si vous supprimez un fichier ou y apportez des modifications accidentellement, vous pouvez utiliser la récupération de fichier pour restaurer le fichier à partir de votre coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="f3804-142">If you accidentally delete or make changes to a file, you can use File Recovery to recover the file from your backup vault.</span></span> <span data-ttu-id="f3804-143">La récupération de fichier utilise un script qui s’exécute sur la machine virtuelle pour monter le point de récupération en tant que lecteur local.</span><span class="sxs-lookup"><span data-stu-id="f3804-143">File Recovery uses a script that runs on the VM, to mount the recovery point as local drive.</span></span> <span data-ttu-id="f3804-144">Ces lecteurs restent montés pendant 12 heures pour vous permettre de copier des fichiers à partir du point de récupération et de les restaurer sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f3804-144">These drives will remain mounted for 12 hours so that you can copy files from the recovery point and restore them to the VM.</span></span>  

<span data-ttu-id="f3804-145">Dans cet exemple, nous allons vous montrer comment récupérer la page web nginx par défaut /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="f3804-145">In this example, we show how to recover the default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="f3804-146">Ici, l’adresse IP publique de notre machine virtuelle est *13.69.75.209*.</span><span class="sxs-lookup"><span data-stu-id="f3804-146">The public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="f3804-147">Vous pouvez trouver l’adresse IP de votre machine virtuelle en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="f3804-147">You can find the IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="f3804-148">Sur votre ordinateur local, ouvrez un navigateur et tapez l’adresse IP publique de votre machine virtuelle pour afficher la page web nginx par défaut.</span><span class="sxs-lookup"><span data-stu-id="f3804-148">On your local computer, open a browser and type in the public IP address of your VM to see the default nginx web page.</span></span>

    ![Page web nginx par défaut](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="f3804-150">Connectez-vous avec SSH à votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f3804-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="f3804-151">Supprimez /var/www/html/index.nginx-debian.html.</span><span class="sxs-lookup"><span data-stu-id="f3804-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="f3804-152">Sur votre ordinateur local, actualisez le navigateur en appuyant sur CTRL + F5 pour confirmer que cette page nginx par défaut a disparu.</span><span class="sxs-lookup"><span data-stu-id="f3804-152">On your local computer, refresh the browser by hitting CTRL + F5 to see that default nginx page is gone.</span></span>

    ![Page web nginx par défaut](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="f3804-154">Sur votre ordinateur local, connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f3804-154">On your local computer, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="f3804-155">Dans le menu de gauche, sélectionnez **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="f3804-155">In the menu on the left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="f3804-156">Sélectionnez la machine virtuelle dans la liste.</span><span class="sxs-lookup"><span data-stu-id="f3804-156">From the list, select the VM.</span></span>
8. <span data-ttu-id="f3804-157">Dans le panneau de la machine virtuelle, au niveau de la section **Paramètres**, cliquez sur **Sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="f3804-157">On the VM blade, in the **Settings** section, click **Backup**.</span></span> <span data-ttu-id="f3804-158">Le panneau **Sauvegarde** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="f3804-158">The **Backup** blade opens.</span></span> 
9. <span data-ttu-id="f3804-159">Dans le menu en haut du panneau, sélectionnez **Récupération de fichier**.</span><span class="sxs-lookup"><span data-stu-id="f3804-159">In the menu at the top of the blade, select **File Recovery**.</span></span> <span data-ttu-id="f3804-160">Le panneau **Récupération de fichier** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="f3804-160">The **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="f3804-161">Dans **Étape 1 : Sélectionner un point de récupération**, sélectionnez un point de récupération dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="f3804-161">In **Step 1: Select recovery point**, select a recovery point from the drop-down.</span></span>
11. <span data-ttu-id="f3804-162">Dans **Étape 2 : Télécharger le script pour parcourir et restaurer des fichiers**, cliquez sur le bouton **Télécharger le fichier exécutable**.</span><span class="sxs-lookup"><span data-stu-id="f3804-162">In **Step 2: Download script to browse and recover files**, click the **Download Executable** button.</span></span> <span data-ttu-id="f3804-163">Enregistrez le fichier téléchargé sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="f3804-163">Save the downloaded file to your local computer.</span></span>
7. <span data-ttu-id="f3804-164">Cliquez sur **Télécharger le script** pour télécharger le fichier de script localement.</span><span class="sxs-lookup"><span data-stu-id="f3804-164">Click **Download script** to download the script file locally.</span></span>
8. <span data-ttu-id="f3804-165">Ouvrez une invite bash et tapez la commande suivante, en remplaçant *Linux_myVM_05-05-2017.sh* par le chemin et le nom de fichier du script que vous avez téléchargé, *azureuser* par le nom d’utilisateur de la machine virtuelle, et *13.69.75.209* par l’adresse IP publique de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f3804-165">Open a Bash prompt and type the following, replacing *Linux_myVM_05-05-2017.sh* with the correct path and filename for the script that you downloaded, *azureuser* with the username for the VM and *13.69.75.209* with the public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="f3804-166">Sur votre ordinateur local, ouvrez une connexion SSH vers la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f3804-166">On your local computer, open an SSH connection to the VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="f3804-167">Sur votre machine virtuelle, ajoutez des autorisations d’exécution au fichier de script.</span><span class="sxs-lookup"><span data-stu-id="f3804-167">On your VM, add execute permissions to the script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="f3804-168">Sur votre machine virtuelle, exécutez le script pour monter le point de récupération comme un système de fichiers.</span><span class="sxs-lookup"><span data-stu-id="f3804-168">On your VM, run the script to mount the recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="f3804-169">La sortie du script vous donne le chemin d’accès pour le point de montage.</span><span class="sxs-lookup"><span data-stu-id="f3804-169">The output from the script gives you the path for the mount point.</span></span> <span data-ttu-id="f3804-170">Le résultat ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="f3804-170">The output looks similar to this:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting to recovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of the recovery point to this machine...
                         
    ************ Volumes of the recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer to browse for files. ************

    After recovery, to remove the disks and close the connection to the recovery point, please click 'Unmount Disks' in step 3 of the portal.

    Please enter 'q/Q' to exit...
    ```

12. <span data-ttu-id="f3804-171">Sur votre machine virtuelle, copiez la page web nginx par défaut du point de montage vers l’emplacement où vous avez supprimé le fichier.</span><span class="sxs-lookup"><span data-stu-id="f3804-171">On your VM, copy the nginx default web page from the mount point back to where you deleted the file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="f3804-172">Sur votre ordinateur local, ouvrez l’onglet du navigateur dans lequel vous êtes connecté à l’adresse IP de la machine virtuelle affichant la page nginx par défaut.</span><span class="sxs-lookup"><span data-stu-id="f3804-172">On your local computer, open the browser tab where you are connected to the IP address of the VM showing the nginx default page.</span></span> <span data-ttu-id="f3804-173">Appuyez sur CTRL + F5 pour actualiser la page du navigateur.</span><span class="sxs-lookup"><span data-stu-id="f3804-173">Press CTRL + F5 to refresh the browser page.</span></span> <span data-ttu-id="f3804-174">Vous devriez maintenant voir que la page par défaut fonctionne à nouveau.</span><span class="sxs-lookup"><span data-stu-id="f3804-174">You should now see that the default page is working again.</span></span>

    ![Page web nginx par défaut](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="f3804-176">Sur votre ordinateur local, revenez à l’onglet du navigateur pour afficher le portail Azure, puis dans **Étape 3 : Démonter les disques après la récupération**, cliquez sur le bouton **Démonter les disques**.</span><span class="sxs-lookup"><span data-stu-id="f3804-176">On your local computer, go back to the browser tab for the Azure portal and in **Step 3: Unmount the disks after recovery** click the **Unmount Disks** button.</span></span> <span data-ttu-id="f3804-177">Si vous avez omis cette étape, la connexion au point de montage est automatiquement fermée après 12 heures.</span><span class="sxs-lookup"><span data-stu-id="f3804-177">If you forget to do this step, the connection to the mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="f3804-178">Une fois ces 12 heures écoulées, vous devez télécharger un nouveau script pour créer un nouveau point de montage.</span><span class="sxs-lookup"><span data-stu-id="f3804-178">After those 12 hours, you need to download a new script to create a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f3804-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f3804-179">Next steps</span></span>

<span data-ttu-id="f3804-180">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="f3804-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f3804-181">Créer une sauvegarde de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="f3804-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="f3804-182">Planifier une sauvegarde quotidienne</span><span class="sxs-lookup"><span data-stu-id="f3804-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="f3804-183">Restaurer un fichier à partir d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="f3804-183">Restore a file from a backup</span></span>

<span data-ttu-id="f3804-184">Passez au didacticiel suivant pour en savoir plus sur la surveillance des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="f3804-184">Advance to the next tutorial to learn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f3804-185">Surveiller les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="f3804-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)

