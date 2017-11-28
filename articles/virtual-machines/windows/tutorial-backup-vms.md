---
title: aaaBackup les machines virtuelles Windows Azure | Des documents Microsoft
description: "Protégez vos machines virtuelles Windows en les sauvegardant à l’aide de Sauvegarde Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="1c49b-103">Sauvegarde de machines virtuelles Windows dans Azure</span><span class="sxs-lookup"><span data-stu-id="1c49b-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="1c49b-104">Vous pouvez protéger vos données en effectuant des sauvegardes à intervalles réguliers.</span><span class="sxs-lookup"><span data-stu-id="1c49b-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="1c49b-105">Azure Backup crée des points de récupération stockés dans des coffres de récupération géoredondants.</span><span class="sxs-lookup"><span data-stu-id="1c49b-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="1c49b-106">Lorsque vous restaurez à partir d’un point de récupération, vous pouvez restaurer hello toute machine virtuelle ou des fichiers spécifiques.</span><span class="sxs-lookup"><span data-stu-id="1c49b-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="1c49b-107">Cet article explique comment toorestore un seul fichier tooa machine virtuelle exécutant Windows Server et IIS.</span><span class="sxs-lookup"><span data-stu-id="1c49b-107">This article explains how toorestore a single file tooa VM running Windows Server and IIS.</span></span> <span data-ttu-id="1c49b-108">Si vous n’avez pas encore un toouse de machine virtuelle, vous pouvez en créer un à l’aide de hello [démarrage rapide de Windows](quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1c49b-108">If you don't already have a VM toouse, you can create one using hello [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="1c49b-109">Ce didacticiel vous explique comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="1c49b-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1c49b-110">Créer une sauvegarde de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1c49b-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="1c49b-111">Planifier une sauvegarde quotidienne</span><span class="sxs-lookup"><span data-stu-id="1c49b-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="1c49b-112">Restaurer un fichier à partir d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="1c49b-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="1c49b-113">Présentation de la sauvegarde</span><span class="sxs-lookup"><span data-stu-id="1c49b-113">Backup overview</span></span>

<span data-ttu-id="1c49b-114">Hello service Azure Backup lorsqu’une opération de sauvegarde, il déclenche hello extension de sauvegarde tootake un instantané de point-à-temps.</span><span class="sxs-lookup"><span data-stu-id="1c49b-114">When hello Azure Backup service initiates a backup job, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="1c49b-115">Hello service Azure Backup utilise hello _VMSnapshot_ extension.</span><span class="sxs-lookup"><span data-stu-id="1c49b-115">hello Azure Backup service uses hello _VMSnapshot_ extension.</span></span> <span data-ttu-id="1c49b-116">extension de Hello est installée au cours de la première sauvegarde de machine virtuelle hello si hello machine virtuelle est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="1c49b-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="1c49b-117">Si hello machine virtuelle ne fonctionne pas, hello service de sauvegarde prend un instantané de hello stockage sous-jacent (dans la mesure où aucune écriture de l’application se produire lors de la machine virtuelle est arrêtée de hello).</span><span class="sxs-lookup"><span data-stu-id="1c49b-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="1c49b-118">Lorsque vous prenez un instantané de machines virtuelles Windows, service de sauvegarde hello coordonne hello Volume Shadow Copy Service (VSS) tooget un instantané cohérent des disques de l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="1c49b-118">When taking a snapshot of Windows VMs, hello Backup service coordinates with hello Volume Shadow Copy Service (VSS) tooget a consistent snapshot of hello virtual machine's disks.</span></span> <span data-ttu-id="1c49b-119">Une fois que hello service Azure Backup prend un instantané de hello, données de hello sont transférées toohello coffre.</span><span class="sxs-lookup"><span data-stu-id="1c49b-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="1c49b-120">l’efficacité toomaximize, hello service identifie et transfère uniquement les blocs de hello de données qui ont été modifiés depuis la sauvegarde précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="1c49b-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="1c49b-121">Lorsque le transfert de données hello est terminé, les instantanés hello sont supprimé et un point de récupération est créé.</span><span class="sxs-lookup"><span data-stu-id="1c49b-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="1c49b-122">Création d'une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="1c49b-122">Create a backup</span></span>
<span data-ttu-id="1c49b-123">Créer une simple planifiée quotidienne sauvegarde tooa coffre Recovery Services.</span><span class="sxs-lookup"><span data-stu-id="1c49b-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="1c49b-124">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1c49b-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1c49b-125">Dans le menu hello hello gauche, sélectionnez **virtuels**.</span><span class="sxs-lookup"><span data-stu-id="1c49b-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="1c49b-126">À partir de la liste de hello, sélectionnez un tooback de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1c49b-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="1c49b-127">Dans Panneau de machine virtuelle hello, Bonjour **paramètres** , cliquez sur **sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="1c49b-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="1c49b-128">Hello **Active la sauvegarde** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="1c49b-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="1c49b-129">Dans **de coffre Recovery Services**, cliquez sur **nouvel** et fournir le nom hello pour le coffre hello.</span><span class="sxs-lookup"><span data-stu-id="1c49b-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="1c49b-130">Un nouvel archivage est créé dans hello même groupe de ressources et l’emplacement en tant que machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="1c49b-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="1c49b-131">Cliquez sur **Stratégie de sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="1c49b-131">Click **Backup policy**.</span></span> <span data-ttu-id="1c49b-132">Pour cet exemple, conservez les valeurs par défaut hello et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="1c49b-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="1c49b-133">Sur hello **Active la sauvegarde** panneau, cliquez sur **activez la sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="1c49b-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="1c49b-134">Cette opération crée une sauvegarde quotidienne selon une planification par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="1c49b-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="1c49b-135">toocreate un point de récupération initial sur hello **sauvegarde** cliquez sur le panneau **sauvegarder maintenant**.</span><span class="sxs-lookup"><span data-stu-id="1c49b-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="1c49b-136">Sur hello **sauvegarde maintenant** panneau, cliquez sur icône du calendrier hello, utilisez Bonjour calendrier contrôle tooselect Bonjour dernier jour de ce point de récupération est conservé, puis cliquez sur **sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="1c49b-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="1c49b-137">Bonjour **sauvegarde** panneau pour votre machine virtuelle, vous verrez nombre hello de points de récupération qui sont terminées.</span><span class="sxs-lookup"><span data-stu-id="1c49b-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Points de récupération](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="1c49b-139">première sauvegarde de Hello prend environ 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="1c49b-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="1c49b-140">Continuer toohello la partie suivante de ce didacticiel, une fois la sauvegarde terminée.</span><span class="sxs-lookup"><span data-stu-id="1c49b-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="1c49b-141">Récupérer un fichier</span><span class="sxs-lookup"><span data-stu-id="1c49b-141">Recover a file</span></span>

<span data-ttu-id="1c49b-142">Si vous supprimez ou rendre le fichier tooa des modifications, vous pouvez utiliser le fichier de récupération de fichier toorecover hello votre coffre de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="1c49b-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="1c49b-143">Récupération de fichiers utilise un script qui s’exécute sur hello machine virtuelle, point de récupération toomount hello en tant que lecteur local.</span><span class="sxs-lookup"><span data-stu-id="1c49b-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="1c49b-144">Ces lecteurs restera montés pendant 12 heures, afin que vous pouvez copier les fichiers de point de récupération hello et restaurez-les toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1c49b-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="1c49b-145">Dans cet exemple, nous montrons comment toorecover hello fichier image qui est utilisée dans la page web de hello par défaut pour IIS.</span><span class="sxs-lookup"><span data-stu-id="1c49b-145">In this example, we show how toorecover hello image file that is used in hello default web page for IIS.</span></span> 

1. <span data-ttu-id="1c49b-146">Ouvrez un navigateur et se connecter à adresse IP de toohello de page IIS hello VM tooshow hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="1c49b-146">Open a browser and connect toohello IP address of hello VM tooshow hello default IIS page.</span></span>

    ![Page web IIS par défaut](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="1c49b-148">Se connecter toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1c49b-148">Connect toohello VM.</span></span>
3. <span data-ttu-id="1c49b-149">Sur la machine virtuelle de hello, ouvrez **l’Explorateur de fichiers** et de naviguer too\inetpub\wwwroot et supprimer le fichier de hello **iisstart.png**.</span><span class="sxs-lookup"><span data-stu-id="1c49b-149">On hello VM, open **File Explorer** and navigate too\inetpub\wwwroot and delete hello file **iisstart.png**.</span></span>
4. <span data-ttu-id="1c49b-150">Sur votre ordinateur local, l’actualisation hello navigateur toosee qui hello image sur la page d’IIS par défaut hello a disparu.</span><span class="sxs-lookup"><span data-stu-id="1c49b-150">On your local computer, refresh hello browser toosee that hello image on hello default IIS page is gone.</span></span>

    ![Page web IIS par défaut](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="1c49b-152">Sur votre ordinateur local, ouvrez un nouvel onglet et un accédez Bonjour Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c49b-152">On your local computer, open a new tab and go hello hello [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="1c49b-153">Dans le menu hello hello gauche, sélectionnez **virtuels** et sélectionnez hello VM écran hello liste.</span><span class="sxs-lookup"><span data-stu-id="1c49b-153">In hello menu on hello left, select **Virtual machines** and select hello VM form hello list.</span></span>
8. <span data-ttu-id="1c49b-154">Dans Panneau de machine virtuelle hello, Bonjour **paramètres** , cliquez sur **sauvegarde**.</span><span class="sxs-lookup"><span data-stu-id="1c49b-154">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="1c49b-155">Hello **sauvegarde** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="1c49b-155">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="1c49b-156">Dans le menu hello haut hello du Panneau de hello, sélectionnez **récupération de fichier**.</span><span class="sxs-lookup"><span data-stu-id="1c49b-156">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="1c49b-157">Hello **récupération de fichier** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="1c49b-157">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="1c49b-158">Dans **étape 1 : sélectionnez le point de récupération**, sélectionnez un point de récupération à partir de hello de liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="1c49b-158">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="1c49b-159">Dans **étape 2 : télécharger le script toobrowse et récupérer les fichiers**, cliquez sur hello **télécharger le fichier exécutable** bouton.</span><span class="sxs-lookup"><span data-stu-id="1c49b-159">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="1c49b-160">Enregistrer hello fichier tooyour **télécharge** dossier.</span><span class="sxs-lookup"><span data-stu-id="1c49b-160">Save hello file tooyour **Downloads** folder.</span></span>
12. <span data-ttu-id="1c49b-161">Sur votre ordinateur local, ouvrez **l’Explorateur de fichiers** et accédez tooyour **télécharge** dossier et copie hello téléchargé un fichier .exe.</span><span class="sxs-lookup"><span data-stu-id="1c49b-161">On your local computer, open **File Explorer** and navigate tooyour **Downloads** folder and copy hello downloaded .exe file.</span></span> <span data-ttu-id="1c49b-162">nom de fichier Hello sera être préfixé par votre nom d’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="1c49b-162">hello filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="1c49b-163">Sur votre machine virtuelle (sur hello connexion RDP) Coller toohello de fichier .exe hello bureau de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1c49b-163">On your VM (over hello RDP connection) paste hello .exe file toohello Desktop of your VM.</span></span> 
14. <span data-ttu-id="1c49b-164">Accédez bureau toohello de votre machine virtuelle et double-cliquez sur hello .exe.</span><span class="sxs-lookup"><span data-stu-id="1c49b-164">Navigate toohello desktop of your VM and double-click on hello .exe.</span></span> <span data-ttu-id="1c49b-165">Vous lancez une invite de commandes et puis montez le point de récupération hello en tant que vous pouvez accéder à un partage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="1c49b-165">This will launch a command prompt and then mount hello recovery point as a file share that you can access.</span></span> <span data-ttu-id="1c49b-166">Quand elle est terminée création hello partage, tapez **q** tooclose hello invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="1c49b-166">When it is finished creating hello share, type **q** tooclose hello command prompt.</span></span>
15. <span data-ttu-id="1c49b-167">Sur votre machine virtuelle, ouvrez **l’Explorateur de fichiers** et accédez de lettre de lecteur toohello qui a été utilisé pour le partage de fichiers hello.</span><span class="sxs-lookup"><span data-stu-id="1c49b-167">On your VM, open **File Explorer** and navigate toohello drive letter that was used for hello file share.</span></span>
16. <span data-ttu-id="1c49b-168">Accédez too\inetpub\wwwroot et copie **iisstart.png** à partir du fichier de hello partager et collez-le dans \inetpub\wwwroot.</span><span class="sxs-lookup"><span data-stu-id="1c49b-168">Navigate too\inetpub\wwwroot and copy **iisstart.png** from hello file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="1c49b-169">Par exemple, copiez F:\inetpub\wwwroot\iisstart.png et collez-le dans le fichier de hello toorecover c:\inetpub\wwwroot.</span><span class="sxs-lookup"><span data-stu-id="1c49b-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot toorecover hello file.</span></span>
17. <span data-ttu-id="1c49b-170">Sur votre ordinateur local, ouvrez l’onglet de navigateur hello où vous êtes connecté adresse toohello de hello VM écran hello IIS par défaut de la page.</span><span class="sxs-lookup"><span data-stu-id="1c49b-170">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello IIS default page.</span></span> <span data-ttu-id="1c49b-171">Appuyez sur CTRL + F5 page du navigateur toorefresh hello.</span><span class="sxs-lookup"><span data-stu-id="1c49b-171">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="1c49b-172">Vous devez maintenant voir que hello image a été restaurée.</span><span class="sxs-lookup"><span data-stu-id="1c49b-172">You should now see that hello image has been restored.</span></span>
18. <span data-ttu-id="1c49b-173">Sur votre ordinateur local, revenir en arrière toohello onglet du navigateur pour hello portail Azure et dans **étape 3 : démontage de disques de hello après la récupération** cliquez sur hello **démontage de disques** bouton.</span><span class="sxs-lookup"><span data-stu-id="1c49b-173">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="1c49b-174">Si vous oubliez toodo cette étape, point de montage toohello hello connexion est automatiquement fermée après 12 heures.</span><span class="sxs-lookup"><span data-stu-id="1c49b-174">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="1c49b-175">Après les 12 heures, vous devez toodownload une nouvelle toocreate de script un nouveau point de montage.</span><span class="sxs-lookup"><span data-stu-id="1c49b-175">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1c49b-176">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1c49b-176">Next steps</span></span>

<span data-ttu-id="1c49b-177">Dans ce didacticiel, vous avez appris à :</span><span class="sxs-lookup"><span data-stu-id="1c49b-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1c49b-178">Créer une sauvegarde de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="1c49b-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="1c49b-179">Planifier une sauvegarde quotidienne</span><span class="sxs-lookup"><span data-stu-id="1c49b-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="1c49b-180">Restaurer un fichier à partir d’une sauvegarde</span><span class="sxs-lookup"><span data-stu-id="1c49b-180">Restore a file from a backup</span></span>

<span data-ttu-id="1c49b-181">Avance toohello toolearn de didacticiel suivant sur l’analyse des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="1c49b-181">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1c49b-182">Surveiller les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="1c49b-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)









