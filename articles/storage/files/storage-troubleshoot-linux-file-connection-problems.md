---
title: "problèmes de stockage de fichier Azure aaaTroubleshoot dans Linux | Documents Microsoft"
description: "Résolution des problèmes liés au stockage Azure File dans Linux"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 4bdc3c6ed2e48f245060a03632fca9bd14d33545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="4bab2-103">Résoudre les problèmes liés au stockage Azure File dans Linux</span><span class="sxs-lookup"><span data-stu-id="4bab2-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="4bab2-104">Cet article répertorie les problèmes courants qui sont associé tooMicrosoft de stockage de fichier Azure lorsque vous vous connectez à partir de clients de Linux.</span><span class="sxs-lookup"><span data-stu-id="4bab2-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="4bab2-105">Il fournit également les causes possibles et les solutions de ces problèmes.</span><span class="sxs-lookup"><span data-stu-id="4bab2-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a><span data-ttu-id="4bab2-106">« quota de disque [autorisation refusée] dépassé » lorsque vous essayez de tooopen un fichier</span><span class="sxs-lookup"><span data-stu-id="4bab2-106">"[permission denied] Disk quota exceeded" when you try tooopen a file</span></span>

<span data-ttu-id="4bab2-107">Sous Linux, vous recevez un message d’erreur similaire hello suivant :</span><span class="sxs-lookup"><span data-stu-id="4bab2-107">In Linux, you receive an error message that resembles hello following:</span></span>

<span data-ttu-id="4bab2-108">**<filename> [autorisation refusée] Quota de disque dépassé**</span><span class="sxs-lookup"><span data-stu-id="4bab2-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="4bab2-109">Cause :</span><span class="sxs-lookup"><span data-stu-id="4bab2-109">Cause</span></span>

<span data-ttu-id="4bab2-110">Vous avez atteint la limite supérieure de hello de handles ouverts simultanées autorisées pour un fichier.</span><span class="sxs-lookup"><span data-stu-id="4bab2-110">You have reached hello upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="4bab2-111">Solution</span><span class="sxs-lookup"><span data-stu-id="4bab2-111">Solution</span></span>

<span data-ttu-id="4bab2-112">Réduire le nombre hello de handles ouverts simultanées en fermant certaines poignées, puis recommencez hello.</span><span class="sxs-lookup"><span data-stu-id="4bab2-112">Reduce hello number of concurrent open handles by closing some handles, and then retry hello operation.</span></span> <span data-ttu-id="4bab2-113">Pour plus d’informations, consultez [Liste de contrôle des performances et de l’extensibilité de Microsoft Azure Storage](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4bab2-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](../common/storage-performance-checklist.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a><span data-ttu-id="4bab2-114">Fichier lente copie tooand à partir du stockage de fichiers Azure Linux</span><span class="sxs-lookup"><span data-stu-id="4bab2-114">Slow file copying tooand from Azure File storage in Linux</span></span>

-   <span data-ttu-id="4bab2-115">Si vous n’avez pas une exigence de taille d’e/s minimale spécifique, nous recommandons d’utiliser 1 Mo comme hello taille d’e/s pour des performances optimales.</span><span class="sxs-lookup"><span data-stu-id="4bab2-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="4bab2-116">Si vous connaissez la taille finale de hello d’un fichier que vous étendez à l’aide des écritures et votre logiciel de ne rencontrer des problèmes de compatibilité lorsqu’une fin non écrit sur le fichier de hello contient des zéros non significatifs, puis définissez une taille de fichier hello à l’avance, au lieu d’apporter à chaque écriture d’une extension écriture.</span><span class="sxs-lookup"><span data-stu-id="4bab2-116">If you know hello final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="4bab2-117">Utilisez hello droite copy (méthode) :</span><span class="sxs-lookup"><span data-stu-id="4bab2-117">Use hello right copy method:</span></span>
    -   <span data-ttu-id="4bab2-118">Utilisez [AZCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) pour les transferts entre deux partages de fichiers.</span><span class="sxs-lookup"><span data-stu-id="4bab2-118">Use [AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="4bab2-119">Utilisez [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre les partages de fichiers sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="4bab2-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="4bab2-120">« Erreur de montage (112) : l’hôte est hors service » en raison d’un délai d’expiration de reconnexion</span><span class="sxs-lookup"><span data-stu-id="4bab2-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="4bab2-121">Une erreur de montage « 112 » se produit sur le client Linux de hello lorsque le client de hello a été inactif pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="4bab2-121">A "112" mount error occurs on hello Linux client when hello client has been idle for a long time.</span></span> <span data-ttu-id="4bab2-122">Après la durée d’inactivité prolongée, hello client se déconnecte et hello connexion expire.</span><span class="sxs-lookup"><span data-stu-id="4bab2-122">After extended idle time, hello client disconnects and hello connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="4bab2-123">Cause :</span><span class="sxs-lookup"><span data-stu-id="4bab2-123">Cause</span></span>

<span data-ttu-id="4bab2-124">connexion de Hello peut être inactive pour hello suivant raisons :</span><span class="sxs-lookup"><span data-stu-id="4bab2-124">hello connection can be idle for hello following reasons:</span></span>

-   <span data-ttu-id="4bab2-125">Problèmes de communication réseau qui empêchent de rétablir un serveur toohello de connexion TCP lorsque l’option de montage « soft » hello par défaut est utilisée</span><span class="sxs-lookup"><span data-stu-id="4bab2-125">Network communication failures that prevent re-establishing a TCP connection toohello server when hello default “soft” mount option is used</span></span>
-   <span data-ttu-id="4bab2-126">Les correctifs de reconnexion récents qui ne sont pas présents dans les anciens noyaux.</span><span class="sxs-lookup"><span data-stu-id="4bab2-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="4bab2-127">Solution</span><span class="sxs-lookup"><span data-stu-id="4bab2-127">Solution</span></span>

<span data-ttu-id="4bab2-128">Ce problème de reconnexion dans le noyau Linux hello a été corrigé dans le cadre de hello modifications suivantes :</span><span class="sxs-lookup"><span data-stu-id="4bab2-128">This reconnection problem in hello Linux kernel is now fixed as part of hello following changes:</span></span>

- [<span data-ttu-id="4bab2-129">Correctif reconnecter toonot différer smb3 session reconnecter longtemps après la reconnexion de socket</span><span class="sxs-lookup"><span data-stu-id="4bab2-129">Fix reconnect toonot defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [<span data-ttu-id="4bab2-130">Appeler le service d’écho immédiatement après la reconnexion du socket</span><span class="sxs-lookup"><span data-stu-id="4bab2-130">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [<span data-ttu-id="4bab2-131">CIFS : Corriger une éventuelle corruption de la mémoire lors de la reconnexion</span><span class="sxs-lookup"><span data-stu-id="4bab2-131">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   <span data-ttu-id="4bab2-132">[CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later) (CIFS : corriger un éventuel double verrouillage du mutex lors de la reconnexion [pour les noyaux v4.9 et ultérieurs])](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)</span><span class="sxs-lookup"><span data-stu-id="4bab2-132">[CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)</span></span>

<span data-ttu-id="4bab2-133">Toutefois, ces modifications ne peuvent pas être déplacées encore tooall hello distributions Linux.</span><span class="sxs-lookup"><span data-stu-id="4bab2-133">However, these changes might not be ported yet tooall hello Linux distributions.</span></span> <span data-ttu-id="4bab2-134">Ce correctif et autres correctifs de reconnexion sont effectuées dans hello suivant populaires noyaux Linux : 4.4.40, 4.8.16 et 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="4bab2-134">This fix and other reconnection fixes are made in hello following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="4bab2-135">Vous pouvez obtenir ce correctif par tooone de ces versions du noyau recommandée de la mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="4bab2-135">You can get this fix by upgrading tooone of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="4bab2-136">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="4bab2-136">Workaround</span></span>

<span data-ttu-id="4bab2-137">Vous pouvez contourner ce problème en spécifiant un montage inconditionnel.</span><span class="sxs-lookup"><span data-stu-id="4bab2-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="4bab2-138">Cette opération force hello client toowait jusqu'à ce qu’une connexion est établie, ou jusqu'à ce qu’elle est interrompue explicitement et peut être utilisé tooprevent erreurs en raison des délais d’expiration réseau.</span><span class="sxs-lookup"><span data-stu-id="4bab2-138">This forces hello client toowait until a connection is established or until it’s explicitly interrupted and can be used tooprevent errors because of network time-outs.</span></span> <span data-ttu-id="4bab2-139">Toutefois, cette solution de contournement peut provoquer des attentes indéfinies.</span><span class="sxs-lookup"><span data-stu-id="4bab2-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="4bab2-140">Être connexions toostop préparée selon les besoins.</span><span class="sxs-lookup"><span data-stu-id="4bab2-140">Be prepared toostop connections as necessary.</span></span>

<span data-ttu-id="4bab2-141">Si vous ne peut pas mettre à niveau des dernières versions de noyau toohello, vous pouvez contourner ce problème en conservant un fichier dans le partage de fichiers Azure hello écrire tooevery 30 secondes ou moins.</span><span class="sxs-lookup"><span data-stu-id="4bab2-141">If you cannot upgrade toohello latest kernel versions, you can work around this problem by keeping a file in hello Azure file share that you write tooevery 30 seconds or less.</span></span> <span data-ttu-id="4bab2-142">Ce doit être une opération d’écriture, telles que la réécriture hello créé ou date de modification sur le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="4bab2-142">This must be a write operation, such as rewriting hello created or modified date on hello file.</span></span> <span data-ttu-id="4bab2-143">Sinon, vous pouvez obtenir des résultats mis en cache, et votre opération ne peut pas déclencher la reconnexion hello.</span><span class="sxs-lookup"><span data-stu-id="4bab2-143">Otherwise, you might get cached results, and your operation might not trigger hello reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="4bab2-144">« Erreur de montage (115) : l’opération est en cours » lorsque vous montez le stockage Azure File à l’aide de SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="4bab2-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="4bab2-145">Cause :</span><span class="sxs-lookup"><span data-stu-id="4bab2-145">Cause</span></span>

<span data-ttu-id="4bab2-146">Certaines distributions Linux ne prennent pas encore en charge les fonctionnalités de chiffrement dans SMB 3.0 et les utilisateurs recevront un message d’erreur « 115 » s’ils tentent de stockage de fichier Azure toomount à l’aide de SMB 3.0 en raison d’une fonctionnalité manquante.</span><span class="sxs-lookup"><span data-stu-id="4bab2-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try toomount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="4bab2-147">Solution</span><span class="sxs-lookup"><span data-stu-id="4bab2-147">Solution</span></span>

<span data-ttu-id="4bab2-148">La fonctionnalité de chiffrement pour SMB 3.0 pour Linux a été introduite dans le noyau 4.11.</span><span class="sxs-lookup"><span data-stu-id="4bab2-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="4bab2-149">Cette fonctionnalité permet le montage du partage de fichiers Azure en local ou à partir d’une autre région Azure.</span><span class="sxs-lookup"><span data-stu-id="4bab2-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="4bab2-150">Au moment de hello du processus de publication, cette fonctionnalité a été utilisées tooUbuntu 17.04 et Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="4bab2-150">At hello time of publishing, this functionality has been backported tooUbuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="4bab2-151">Si votre client Linux SMB ne prend pas en charge le chiffrement, montez le stockage Azure à l’aide de SMB 2.1 à partir d’une machine virtuelle Linux Azure qui se trouve dans hello même centre de données comme hello compte de stockage de fichiers.</span><span class="sxs-lookup"><span data-stu-id="4bab2-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in hello same datacenter as hello File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="4bab2-152">Ralentissement des performances dans un partage de fichiers Azure monté sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4bab2-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="4bab2-153">Cause :</span><span class="sxs-lookup"><span data-stu-id="4bab2-153">Cause</span></span>

<span data-ttu-id="4bab2-154">L’une des causes possibles du ralentissement des performances est la désactivation de la mise en cache.</span><span class="sxs-lookup"><span data-stu-id="4bab2-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="4bab2-155">Solution</span><span class="sxs-lookup"><span data-stu-id="4bab2-155">Solution</span></span>

<span data-ttu-id="4bab2-156">toocheck si la mise en cache est désactivée, recherchez hello **cache =** entrée.</span><span class="sxs-lookup"><span data-stu-id="4bab2-156">toocheck whether caching is disabled, look for hello **cache=** entry.</span></span> 

<span data-ttu-id="4bab2-157">**cache=none** indique que la mise en cache est désactivée.</span><span class="sxs-lookup"><span data-stu-id="4bab2-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="4bab2-158">Remontage hello partage à l’aide de la commande de montage hello par défaut ou en ajoutant explicitement hello **cache = strict** option toohello montage commande tooensure par défaut le mode de mise en cache de mise en cache ou « strict » est activée.</span><span class="sxs-lookup"><span data-stu-id="4bab2-158">Remount hello share by using hello default mount command or by explicitly adding hello **cache=strict** option toohello mount command tooensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="4bab2-159">Dans certains scénarios, hello **serverino** montage option peut entraîner une hello **ls** stat toorun de commande par rapport à chaque entrée de répertoire.</span><span class="sxs-lookup"><span data-stu-id="4bab2-159">In some scenarios, hello **serverino** mount option can cause hello **ls** command toorun stat against every directory entry.</span></span> <span data-ttu-id="4bab2-160">Ce comportement provoque une dégradation des performances lorsque vous répertoriez le contenu d’un répertoire volumineux.</span><span class="sxs-lookup"><span data-stu-id="4bab2-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="4bab2-161">Vous pouvez vérifier les options de montage hello votre **/etc/fstab** entrée :</span><span class="sxs-lookup"><span data-stu-id="4bab2-161">You can check hello mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="4bab2-162">Vous pouvez également vérifier si les options correctes hello sont utilisées en exécutant hello **sudo montage | grep cifs** commande et en vérifiant sa sortie, par exemple hello suivant l’exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="4bab2-162">You can also check whether hello correct options are being used by running hello  **sudo mount | grep cifs** command and checking its output, such as hello following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="4bab2-163">Si hello **cache = strict** ou **serverino** option n’est pas présente, démonter et remonter le stockage Azure en exécutant la commande de montage hello de hello [documentation](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4bab2-163">If hello **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running hello mount command from hello [documentation](../storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="4bab2-164">Ensuite, vérifiez à nouveau ce hello **/etc/fstab** entrée comporte les options correctes hello.</span><span class="sxs-lookup"><span data-stu-id="4bab2-164">Then, recheck that hello **/etc/fstab** entry has hello correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a><span data-ttu-id="4bab2-165">Horodatages ont été perdues lors de la copie des fichiers à partir de Windows tooLinux</span><span class="sxs-lookup"><span data-stu-id="4bab2-165">Time stamps were lost in copying files from Windows tooLinux</span></span>

<span data-ttu-id="4bab2-166">Sur les plateformes Linux/Unix, hello **cp -p** commande échoue si le fichier 1 et 2 sont détenus par différents utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="4bab2-166">On Linux/Unix platforms, hello **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="4bab2-167">Cause :</span><span class="sxs-lookup"><span data-stu-id="4bab2-167">Cause</span></span>

<span data-ttu-id="4bab2-168">Hello indicateur force **f** dans COPYFILE provoque l’exécution de **cp -p -f** sous Unix.</span><span class="sxs-lookup"><span data-stu-id="4bab2-168">hello force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="4bab2-169">Cette commande échoue également horodatage toopreserve hello du fichier hello dont vous n’êtes pas propriétaire.</span><span class="sxs-lookup"><span data-stu-id="4bab2-169">This command also fails toopreserve hello time stamp of hello file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="4bab2-170">Solution de contournement</span><span class="sxs-lookup"><span data-stu-id="4bab2-170">Workaround</span></span>

<span data-ttu-id="4bab2-171">Utilisez l’utilisateur du compte de stockage hello pour copier des fichiers de hello :</span><span class="sxs-lookup"><span data-stu-id="4bab2-171">Use hello storage account user for copying hello files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="4bab2-172">Vous avez besoin d’aide ?</span><span class="sxs-lookup"><span data-stu-id="4bab2-172">Need help?</span></span> <span data-ttu-id="4bab2-173">Contactez le support technique.</span><span class="sxs-lookup"><span data-stu-id="4bab2-173">Contact support.</span></span>

<span data-ttu-id="4bab2-174">Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.</span><span class="sxs-lookup"><span data-stu-id="4bab2-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
