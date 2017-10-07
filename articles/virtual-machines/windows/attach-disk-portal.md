---
title: "aaaAttach un tooa de disque des données non managées machine virtuelle Windows - Azure | Documents Microsoft"
description: "Comment tooattach nouvelle ou existante de données non managées disque tooa machine virtuelle Windows dans le portail Azure à l’aide de hello hello modèle de déploiement de gestionnaire de ressources."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3790fc59-7264-41df-b7a3-8d1226799885
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: cynthn
ms.openlocfilehash: 923a6663974143bf359970f9b0eb0d36cabcba9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooattach-an-unmanaged-data-disk-tooa-windows-vm-in-hello-azure-portal"></a>Tooattach une données non managées de disque tooa machine virtuelle Windows dans hello portail Azure

Cet article explique comment tooattach nouvel et existante non managée de disques virtuels tooWindows via hello portail Azure. Vous pouvez également [attacher un disque de données à l’aide de PowerShell](./attach-disk-ps.md). Avant cela, passez en revue les conseils suivants :

* taille de Hello de machine virtuelle de hello détermine le nombre que vous pouvez attacher des disques de données. Pour en savoir plus, voir la rubrique [Tailles de machines virtuelles](sizes.md).
* toouse stockage Premium, vous devez un ordinateur virtuel de la série DS ou GS-series. Vous pouvez utiliser des disques de comptes de stockage Premium et Standard avec ces machines virtuelles. Le stockage Premium est disponible dans certaines régions. Pour plus d’informations, voir l’article [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](../../storage/storage-premium-storage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Pour un nouveau disque, vous n’avez pas besoin toocreate il premier, car Azure crée lorsque vous l’attachez.


Vous pouvez également [attacher un disque de données à l’aide de PowerShell](attach-disk-ps.md).


## <a name="find-hello-virtual-machine"></a>Trouver l’ordinateur virtuel de hello
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/).
2. Dans le menu hello hello gauche, cliquez sur **virtuels**.
3. Sélectionnez hello virtuels à partir de la liste de hello.
4. Dans le panneau des machines virtuelles hello, cliquez sur **disques**.
   
Continuez en suivant les instructions pour attacher un [nouveau disque](#option-1-attach-a-new-disk) ou un [disque existant](#option-2-attach-an-existing-disk).

## <a name="option-1-attach-and-initialize-a-new-disk"></a>Option 1 : attacher et initialiser un nouveau disque
1. Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.
2. Bonjour **attacher un disque géré** panneau, tapez un nom pour le disque hello dans **nom** , puis sélectionnez **nouveau (disque vide)** dans **type de Source**.
3. Sous **conteneur de stockage**, cliquez sur hello **Parcourir** bouton et parcourir le compte de stockage toohello et le conteneur où vous serez hello nouveau disque dur virtuel toobe est stocké et puis cliquez sur **sélectionnez**. 
  
   ![Examen des paramètres d’un disque](./media/attach-disk-portal/attach-empty-unmanaged.png)
   
3. Lorsque vous avez terminé avec les paramètres de hello hello disque de données, cliquez sur **OK**.
4. Dans hello **disques** panneau, cliquez sur **enregistrer** configuration d’ordinateur virtuel toohello disque tooadd hello.


### <a name="initialize-a-new-data-disk"></a>Initialisation d’un nouveau disque de données

1. Connecter l’ordinateur virtuel de toohello. Pour obtenir des instructions, consultez [comment tooconnect et ouverture de session tooan Azure virtual machine exécutant Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
1. Cliquez sur hello **Démarrer** menu hello machine virtuelle et type **diskmgmt.msc** puis appuyez sur **entrée**. Cela démarre le composant logiciel enfichable Gestion des disques hello.
2. Gestion des disques reconnaît que vous avez un disque non initialisé et hello initialiser le disque fenêtre s’affiche.
3. Assurez-vous que le nouveau disque de hello est sélectionné et cliquez sur **OK** tooinitialize il.
4. Hello nouveau disque apparaît désormais comme **non alloué**. Avec le bouton droit n’importe où sur le disque de hello et sélectionnez **nouveau volume simple**. Hello **Assistant de nouveau Volume Simple** démarre.
5. Passez en revue l’Assistant hello, conserve toutes les valeurs par défaut de hello, lorsque vous avez terminé de sélectionner **Terminer**.
6. Fermez Gestion des disques.
7. Vous obtenez une fenêtre contextuelle vous devez de nouveau disque de tooformat hello avant que vous puissiez l’utiliser. Cliquez sur **Formater le disque**.
8. Bonjour **nouveau disque de Format** boîte de dialogue, vérifiez les paramètres hello et puis cliquez sur **Démarrer**.
9. Vous obtenez un avertissement que le formatage des disques de hello efface toutes les données de salutation, cliquez sur **OK**.
10. Lorsque le format de hello est terminée, cliquez sur **OK**.


## <a name="option-2-attach-an-existing-disk"></a>Option 2 : attacher un disque existant
1. Sur hello **disques** panneau, cliquez sur **+ disque de données ajouter**.
2. Sur hello **attacher un disque non managé** panneau, dans **type de Source de** sélectionnez **existant blob**.

    ![Examen des paramètres d’un disque](./media/attach-disk-portal/attach-existing-unmanaged.png)

    3. Cliquez sur **Parcourir** toonavigate toohello compte de stockage et le conteneur où hello disque dur virtuel existant se trouve. Cliquez sur, hello du disque dur virtuel, puis cliquez **sélectionnez**.
4. Cliquez sur **OK** Bonjour **attacher un disque non managé** panneau.
5. Bonjour **disques** panneau, cliquez sur **enregistrer** tooadd hello toohello configuration des hello machine virtuelle.
   


## <a name="use-trim-with-standard-storage"></a>Utilisation de TRIM avec le stockage standard

Si vous utilisez le stockage standard (disque dur), vous devez activer la fonction TRIM. La fonction TRIM ignore les blocs inutilisés sur le disque de hello afin de vous êtes facturé uniquement pour le stockage que vous utilisez réellement. Vous pouvez ainsi faire des économies si vous créez des fichiers volumineux, puis les supprimez. 

Vous pouvez exécuter ce paramètre de découpage hello commande toocheck. Ouvrez une invite de commandes sur votre machine virtuelle Windows et saisissez :

```
fsutil behavior query DisableDeleteNotify
```

Si la commande hello retourne 0, la fonction TRIM est activée correctement. Si elle retourne 1, exécutez hello suivant commande tooenable d’ajustement :
```
fsutil behavior set DisableDeleteNotify 0
```

Après la suppression des données à partir de votre disque, vous pouvez garantir la défragmentation des opérations de découpage hello vidage correctement en exécutant avec la fonction TRIM :

```
defrag.exe <volume:> -l
```

Vous pouvez également vérifier la totalité du volume hello est tronqué en mettant en forme de volume de hello.


## <a name="next-steps"></a>Étapes suivantes
Si votre application a besoin de données toostore toouse hello D:, vous pouvez [modifier la lettre du lecteur de disque temporaire de Windows hello hello](change-drive-letter.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

