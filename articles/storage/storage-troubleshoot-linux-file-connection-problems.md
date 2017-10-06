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
ms.openlocfilehash: 3dc537d714244451a5ff8e01f4a27f03873cf2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a>Résoudre les problèmes liés au stockage Azure File dans Linux

Cet article répertorie les problèmes courants qui sont associé tooMicrosoft de stockage de fichier Azure lorsque vous vous connectez à partir de clients de Linux. Il fournit également les causes possibles et les solutions de ces problèmes.

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a>« quota de disque [autorisation refusée] dépassé » lorsque vous essayez de tooopen un fichier

Sous Linux, vous recevez un message d’erreur similaire hello suivant :

**<filename> [autorisation refusée] Quota de disque dépassé**

### <a name="cause"></a>Cause :

Vous avez atteint la limite supérieure de hello de handles ouverts simultanées autorisées pour un fichier.

### <a name="solution"></a>Solution

Réduire le nombre hello de handles ouverts simultanées en fermant certaines poignées, puis recommencez hello. Pour plus d’informations, consultez [Liste de contrôle des performances et de l’extensibilité de Microsoft Azure Storage](storage-performance-checklist.md).

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a>Fichier lente copie tooand à partir du stockage de fichiers Azure Linux

-   Si vous n’avez pas une exigence de taille d’e/s minimale spécifique, nous recommandons d’utiliser 1 Mo comme hello taille d’e/s pour des performances optimales.
-   Si vous connaissez la taille finale de hello d’un fichier que vous étendez à l’aide des écritures et votre logiciel de ne rencontrer des problèmes de compatibilité lorsqu’une fin non écrit sur le fichier de hello contient des zéros non significatifs, puis définissez une taille de fichier hello à l’avance, au lieu d’apporter à chaque écriture d’une extension écriture.
-   Utilisez hello droite copy (méthode) :
    -   Utilisez [AZCopy](storage-use-azcopy.md#file-copy) pour les transferts entre deux partages de fichiers.
    -   Utilisez [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) entre les partages de fichiers sur un ordinateur local.

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a>« Erreur de montage (112) : l’hôte est hors service » en raison d’un délai d’expiration de reconnexion

Une erreur de montage « 112 » se produit sur le client Linux de hello lorsque le client de hello a été inactif pendant un certain temps. Après la durée d’inactivité prolongée, hello client se déconnecte et hello connexion expire.  

### <a name="cause"></a>Cause :

connexion de Hello peut être inactive pour hello suivant raisons :

-   Problèmes de communication réseau qui empêchent de rétablir un serveur toohello de connexion TCP lorsque l’option de montage « soft » hello par défaut est utilisée
-   Les correctifs de reconnexion récents qui ne sont pas présents dans les anciens noyaux.

### <a name="solution"></a>Solution

Ce problème de reconnexion dans le noyau Linux hello a été corrigé dans le cadre de hello modifications suivantes :

- [Correctif reconnecter toonot différer smb3 session reconnecter longtemps après la reconnexion de socket](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [Appeler le service d’écho immédiatement après la reconnexion du socket](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [CIFS : Corriger une éventuelle corruption de la mémoire lors de la reconnexion](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later) (CIFS : corriger un éventuel double verrouillage du mutex lors de la reconnexion [pour les noyaux v4.9 et ultérieurs])](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

Toutefois, ces modifications ne peuvent pas être déplacées encore tooall hello distributions Linux. Ce correctif et autres correctifs de reconnexion sont effectuées dans hello suivant populaires noyaux Linux : 4.4.40, 4.8.16 et 4.9.1. Vous pouvez obtenir ce correctif par tooone de ces versions du noyau recommandée de la mise à niveau.

### <a name="workaround"></a>Solution de contournement

Vous pouvez contourner ce problème en spécifiant un montage inconditionnel. Cette opération force hello client toowait jusqu'à ce qu’une connexion est établie, ou jusqu'à ce qu’elle est interrompue explicitement et peut être utilisé tooprevent erreurs en raison des délais d’expiration réseau. Toutefois, cette solution de contournement peut provoquer des attentes indéfinies. Être connexions toostop préparée selon les besoins.

Si vous ne peut pas mettre à niveau des dernières versions de noyau toohello, vous pouvez contourner ce problème en conservant un fichier dans le partage de fichiers Azure hello écrire tooevery 30 secondes ou moins. Ce doit être une opération d’écriture, telles que la réécriture hello créé ou date de modification sur le fichier de hello. Sinon, vous pouvez obtenir des résultats mis en cache, et votre opération ne peut pas déclencher la reconnexion hello.

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a>« Erreur de montage (115) : l’opération est en cours » lorsque vous montez le stockage Azure File à l’aide de SMB 3.0

### <a name="cause"></a>Cause :

Certaines distributions Linux ne prennent pas encore en charge les fonctionnalités de chiffrement dans SMB 3.0 et les utilisateurs recevront un message d’erreur « 115 » s’ils tentent de stockage de fichier Azure toomount à l’aide de SMB 3.0 en raison d’une fonctionnalité manquante.

### <a name="solution"></a>Solution

La fonctionnalité de chiffrement pour SMB 3.0 pour Linux a été introduite dans le noyau 4.11. Cette fonctionnalité permet le montage du partage de fichiers Azure en local ou à partir d’une autre région Azure. Au moment de hello du processus de publication, cette fonctionnalité a été utilisées tooUbuntu 17.04 et Ubuntu 16.10. Si votre client Linux SMB ne prend pas en charge le chiffrement, montez le stockage Azure à l’aide de SMB 2.1 à partir d’une machine virtuelle Linux Azure qui se trouve dans hello même centre de données comme hello compte de stockage de fichiers.

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a>Ralentissement des performances dans un partage de fichiers Azure monté sur une machine virtuelle

### <a name="cause"></a>Cause :

L’une des causes possibles du ralentissement des performances est la désactivation de la mise en cache.

### <a name="solution"></a>Solution

toocheck si la mise en cache est désactivée, recherchez hello **cache =** entrée. 

**cache=none** indique que la mise en cache est désactivée.  Remontage hello partage à l’aide de la commande de montage hello par défaut ou en ajoutant explicitement hello **cache = strict** option toohello montage commande tooensure par défaut le mode de mise en cache de mise en cache ou « strict » est activée.

Dans certains scénarios, hello **serverino** montage option peut entraîner une hello **ls** stat toorun de commande par rapport à chaque entrée de répertoire. Ce comportement provoque une dégradation des performances lorsque vous répertoriez le contenu d’un répertoire volumineux. Vous pouvez vérifier les options de montage hello votre **/etc/fstab** entrée :

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

Vous pouvez également vérifier si les options correctes hello sont utilisées en exécutant hello **sudo montage | grep cifs** commande et en vérifiant sa sortie, par exemple hello suivant l’exemple de sortie :

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

Si hello **cache = strict** ou **serverino** option n’est pas présente, démonter et remonter le stockage Azure en exécutant la commande de montage hello de hello [documentation](storage-how-to-use-files-linux.md). Ensuite, vérifiez à nouveau ce hello **/etc/fstab** entrée comporte les options correctes hello.

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a>Horodatages ont été perdues lors de la copie des fichiers à partir de Windows tooLinux

Sur les plateformes Linux/Unix, hello **cp -p** commande échoue si le fichier 1 et 2 sont détenus par différents utilisateurs.

### <a name="cause"></a>Cause :

Hello indicateur force **f** dans COPYFILE provoque l’exécution de **cp -p -f** sous Unix. Cette commande échoue également horodatage toopreserve hello du fichier hello dont vous n’êtes pas propriétaire.

### <a name="workaround"></a>Solution de contournement

Utilisez l’utilisateur du compte de stockage hello pour copier des fichiers de hello :

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contactez le support technique.

Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.
