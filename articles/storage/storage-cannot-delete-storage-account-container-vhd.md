---
title: "suppression de comptes de stockage Azure, les conteneurs ou les disques durs virtuels dans un déploiement classique d’aaaTroubleshoot | Documents Microsoft"
description: "Résoudre les problèmes de suppression de comptes de stockage Azure, de conteneurs ou de disques durs virtuels dans un déploiement classique"
services: storage
documentationcenter: 
author: genlin
manager: felixwu
editor: tysonn
tags: storage
ms.assetid: 0f7a8243-d8dc-432a-9d37-1272a0cb3a5c
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 6bbfa032e1968718c623227bb426d553e2951075
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deleting-azure-storage-accounts-containers-or-vhds-in-a-classic-deployment"></a>Résoudre les problèmes de suppression de comptes de stockage Azure, de conteneurs ou de disques durs virtuels dans un déploiement classique
[!INCLUDE [storage-selector-cannot-delete-storage-account-container-vhd](../../includes/storage-selector-cannot-delete-storage-account-container-vhd.md)]

Vous pouvez recevoir des erreurs lorsque vous essayez de disque dur virtuel, du conteneur ou compte de stockage Azure hello toodelete Bonjour [portail Azure](https://portal.azure.com/) ou hello [portail Azure classic](https://manage.windowsazure.com/). problèmes de Hello peuvent résulter de hello suivant circonstances :

* Lorsque vous supprimez une machine virtuelle, disque de hello et de disque dur virtuel ne sont pas automatiquement supprimés. Qui peut être la raison hello de défaillance sur la suppression de compte de stockage. Nous ne souhaite pas supprimer le disque de hello afin que vous puissiez utiliser hello disque toomount une autre machine virtuelle.
* Il existe toujours un bail sur un objet blob de disque ou hello associé avec un disque de hello.
* Il existe toujours une image de machine virtuelle qui utilise un compte de stockage, un conteneur ou un objet blob.

Si votre problème Azure n’est pas abordé dans cet article, visitez hello forums Azure sur [MSDN et hello Stack Overflow](https://azure.microsoft.com/support/forums/). Vous pouvez publier votre problème sur ces forums ou too@AzureSupport sur Twitter. En outre, vous pouvez entrer une demande de support Azure en sélectionnant **obtenir un support technique** sur hello [prise en charge Azure](https://azure.microsoft.com/support/options/) site.

## <a name="symptoms"></a>Symptômes
Hello après section répertorie les erreurs courantes susceptibles d’apparaître lorsque vous essayez de comptes de stockage Azure hello toodelete, les conteneurs ou les disques durs virtuels.

### <a name="scenario-1-unable-toodelete-a-storage-account"></a>Scénario 1 : Toodelete Impossible un compte de stockage
Lorsque vous accédez compte de stockage classiques toohello Bonjour [portail Azure](https://portal.azure.com/) et sélectionnez **supprimer**, avec une liste d’objets qui empêchent la suppression du compte de stockage hello peuvent s’afficher :

  ![Image d’erreur lorsque supprimez le compte de stockage hello](./media/storage-cannot-delete-storage-account-container-vhd/newerror.png)

Lorsque vous accédez compte de stockage toohello Bonjour [portail Azure classic](https://manage.windowsazure.com/) et sélectionnez **supprimer**, vous pouvez voir un des hello les erreurs suivantes :

- *Le compte de stockage StorageAccountName contient des images de machine virtuelle. Supprimez ces images de machine virtuelle avant de supprimer ce compte de stockage.*

- *Échec de compte de stockage toodelete < vm-storage-account-name >. Compte de stockage ne peut pas toodelete < vm-storage-account-name > : « compte de stockage < vm-storage-account-name > a certaines images actives et/ou des disques. Supprimez ces images et/ou disques avant de supprimer ce compte de stockage. ».*

- *Le compte de stockage &lt;vm-storage-account-name&gt; contient des images et/ou des disques actifs, par exemple, xxxxxxxxx- xxxxxxxxx-O-209490240936090599. Supprimez ces images et/ou disques avant de supprimer ce compte de stockage.*

- *Le compte de stockage &lt;vm-storage-account-name&gt; contient 1 ou plusieurs conteneurs avec une image active et/ou des artefacts de disque. Vérifiez ces artefacts sont supprimés à partir du référentiel d’images hello avant de supprimer ce compte de stockage*.

- *Échec d’envoi : le compte de stockage &lt;vm-storage-account-name&gt; contient 1 ou plusieurs conteneurs avec une image active et/ou des artefacts de disque. Assurez-vous que ces artefacts sont supprimés à partir du référentiel d’images hello avant de supprimer ce compte de stockage. Lorsque vous essayez de toodelete un compte de stockage et des disques toujours actives associées, vous verrez un message vous indiquant que des disques actifs doivent toobe supprimé*.

### <a name="scenario-2-unable-toodelete-a-container"></a>Scénario 2 : Toodelete Impossible d’un conteneur
Lorsque vous essayez de conteneur de stockage toodelete hello, vous pouvez voir hello l’erreur suivante :

*Conteneur de stockage ayant échoué toodelete <container name>. Erreur : « il existe actuellement un bail sur le conteneur de hello et aucun ID de bail a été spécifié dans la demande hello*.

Ou

*Hello disques de machine virtuelle suivants utilisent les objets BLOB dans ce conteneur, donc impossible de supprimer le conteneur de hello : VirtualMachineDiskName1, VirtualMachineDiskName2,...*

### <a name="scenario-3-unable-toodelete-a-vhd"></a>Scénario 3 : Toodelete Impossible un disque dur virtuel
Une fois que vous supprimez une machine virtuelle, et puis essayez toodelete hello objets BLOB pour hello associées des disques durs virtuels, vous pouvez recevoir hello message suivant :

*Échec toodelete blob ' chemin d’accès/XXXXXX-XXXXXX-os-1447379084699.vhd'. Erreur : « il existe actuellement un bail sur l’objet blob de hello et aucun ID de bail a été spécifié dans la demande hello.*

Ou

*Objet blob 'BlobName.vhd' est en cours d’utilisation en tant que disque de machine virtuelle 'VirtualMachineDiskName', et hello ne peut pas être supprimé.*

## <a name="solution"></a>Solution
problèmes les plus courants tooresolve hello hello try suivant de méthode :

### <a name="step-1-delete-any-disks-that-are-preventing-deletion-of-hello-storage-account-container-or-vhd"></a>Étape 1 : Supprimer tous les disques qui empêchent la suppression du compte de stockage hello, conteneur ou de disque dur virtuel
1. Commutateur toohello [portail Azure classic](https://manage.windowsazure.com/).
2. Sélectionnez **MACHINES VIRTUELLES** > **DISQUES**.

    ![Image de disques sur des machines virtuelles sur le portail Azure Classic.](./media/storage-cannot-delete-storage-account-container-vhd/VMUI.png)
3. Recherchez des disques hello associés hello compte de stockage, conteneur ou disque dur virtuel que vous souhaitez toodelete. Lorsque vous vérifiez emplacement hello du disque de hello, vous constaterez hello associée compte de stockage, conteneur ou disque dur virtuel.

    ![Image qui affiche des informations d'emplacement sur les disques sur le portail Azure Classic](./media/storage-cannot-delete-storage-account-container-vhd/DiskLocation.png)
4. Supprimer les disques hello à l’aide d’une des méthodes suivantes de hello :

  - S’il existe aucune machine virtuelle ne répertoriés sur hello **attaché à** champ du disque de hello, vous pouvez supprimer les disques hello directement.

  - Si hello est un disque de données, procédez comme suit :

    1. Vérifiez le nom de machine virtuelle de ce disque hello de hello hello est attaché à.
    2. Accédez trop**virtuels** > **Instances**, puis recherchez hello machine virtuelle.
    3. Assurez-vous que rien n’est activement à l’aide hello disque.
    4. Sélectionnez **détacher un disque** bas hello du disque de hello toodetach portail hello.
    5. Accédez trop**virtuels** > **disques**et attendez hello **attaché à** tooturn champ vide. Cela indique le disque de hello a été détaché avec succès à partir de la machine virtuelle de hello.
    6. Sélectionnez **supprimer** bas hello **virtuels** > **disques** disque de hello toodelete.

  - Si le disque de hello est un disque de système d’exploitation (hello **contient le système d’exploitation** champ a une valeur comme fenêtres) attaché tooa machine virtuelle, procédez comme suit toodelete hello machine virtuelle. Impossible de détacher le disque du système d’exploitation Hello, afin que nous le bail hello toorelease toodelete hello machine virtuelle.

    1. Vérifiez le nom du hello Hello de Machine virtuelle hello À que disque de données est attachée.  
    2. Accédez trop**virtuels** > **Instances**, et puis sélectionnez hello machine virtuelle qui hello disque est attaché à.
    3. Assurez-vous que rien n’est activement à l’aide de hello d’ordinateurs virtuels et que vous avez besoin n’est plus hello machine virtuelle.
    4. Sélectionnez hello VM hello disque est attaché à, puis sélectionnez **supprimer** > **hello de suppression de disques attachés**.
    5. Accédez trop**virtuels** > **disques**et attendez hello disque toodisappear.  Il peut prendre quelques minutes avant que cette toooccur, et vous devrez peut-être page hello de toorefresh.
    6. Si le disque de hello ne disparaît pas, attendez hello **attaché à** tooturn champ vide. Cela indique que les disques hello a entièrement détaché de hello machine virtuelle.  Ensuite, sélectionnez le disque hello et sélectionnez **supprimer** bas hello hello pages toodelete hello disque.


   > [!NOTE]
   > Si un disque est attaché tooa machine virtuelle, vous ne serez pas en mesure de toodelete il. Les disques sont détachés de façon asynchrone d’une machine virtuelle supprimée. Il peut prendre quelques minutes après que hello machine virtuelle est supprimé pour cette tooclear de champ de.
   >
   >


### <a name="step-2-delete-any-vm-images-that-are-preventing-deletion-of-hello-storage-account-or-container"></a>Étape 2 : Supprimer toutes les Images de machine virtuelle qui empêchent la suppression du compte de stockage hello ou du conteneur
1. Commutateur toohello [portail Azure classic](https://manage.windowsazure.com/).
2. Sélectionnez **virtuels** > **IMAGES**, puis supprimez les images hello associés hello compte de stockage, conteneur ou disque dur virtuel.

    Après cela, essayez à nouveau compte de stockage toodelete hello, du conteneur ou disque dur virtuel.

> [!WARNING]
> Être tooback que rien souhaité toosave avant de supprimer le compte de hello. Lorsque vous supprimez un VHD, un blob, une table, une file d’attente ou un fichier, il est définitivement supprimé. Assurez-vous que les ressources hello ne sont pas en cours d’utilisation.
>
>

## <a name="about-hello-stopped-deallocated-status"></a>À propos de hello arrêté (désallouée) état
Ordinateurs virtuels qui ont été créées dans le modèle de déploiement classique hello et qui ont été conservées aura hello **arrêté (désallouée)** statut soit hello [portail Azure](https://portal.azure.com/) ou [portail Azure classic ](https://manage.windowsazure.com/).

**Portail Azure Classic**:

![Statut Arrêté (désalloué) pour les machines virtuelles sur le portail Azure.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo2.png)

**Portail Azure**:

![Statut Arrêté (désalloué) pour les machines virtuelles sur le portail Azure Classic.](./media/storage-cannot-delete-storage-account-container-vhd/moreinfo1.png)

Un état « Arrêté (désalloué) » libère des ressources d’ordinateur de hello, comme les hello du processeur, mémoire et du réseau. les disques Hello, toutefois, sont toujours conservés afin que vous pouvez rapidement recréer hello machine virtuelle si nécessaire. Ces disques sont créés sur les disques durs virtuels sauvegardés par Azure Storage. compte de stockage Hello a ces disques durs virtuels et des disques hello ont des baux sur ces disques durs virtuels.

## <a name="next-steps"></a>Étapes suivantes
* [Suppression d'un compte de stockage](storage-create-storage-account.md#delete-a-storage-account)
