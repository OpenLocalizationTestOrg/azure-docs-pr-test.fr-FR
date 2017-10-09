---
title: erreurs aaaTroubleshoot lorsque vous supprimez des comptes de stockage Azure, les conteneurs ou les disques durs virtuels | Documents Microsoft
description: "Résoudre les erreurs lorsque vous supprimez des comptes de stockage Azure, des conteneurs ou des disques durs virtuels"
services: storage
documentationcenter: 
author: genlin
manager: cshepard
editor: na
tags: storage
ms.assetid: 17403aa1-fe8d-45ec-bc33-2c0b61126286
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 77361593e2c924d39aba853e0807dc3188f50e60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-errors-when-you-delete-azure-storage-accounts-containers-or-vhds"></a>Résoudre les erreurs lorsque vous supprimez des comptes de stockage Azure, des conteneurs ou des disques durs virtuels

Vous pouvez recevoir des erreurs lorsque vous essayez de toodelete un compte de stockage Azure, un conteneur ou un disque dur virtuel (VHD) Bonjour [portail Azure](https://portal.azure.com). Cet article présente le dépannage des conseils toohelp résolution hello dans un déploiement d’Azure Resource Manager.

Si cet article ne répond pas à votre problème Azure, visitez hello forums Azure sur [MSDN et le débordement de pile](https://azure.microsoft.com/support/forums/). Vous pouvez publier votre problème sur ces forums ou too@AzureSupport sur Twitter. En outre, vous pouvez entrer une demande de support Azure en sélectionnant **obtenir un support technique** sur hello [prise en charge Azure](https://azure.microsoft.com/support/options/) site.

## <a name="symptoms"></a>Symptômes
### <a name="scenario-1"></a>Scénario 1
Lorsque vous essayez de toodelete un disque dur virtuel dans un compte de stockage dans un déploiement du Gestionnaire de ressources, vous recevez hello message d’erreur suivant :

**Échec de l’objet blob de toodelete 'vhds/BlobName.vhd'. Erreur : Il existe actuellement un bail sur l’objet blob de hello et aucun ID de bail a été spécifié dans la demande hello.**

Ce problème peut se produire, car un ordinateur virtuel (VM) a un bail sur hello disque dur virtuel que vous essayez de toodelete.

### <a name="scenario-2"></a>Scénario 2
Lorsque vous essayez de toodelete un conteneur dans un compte de stockage dans un déploiement du Gestionnaire de ressources, vous recevez hello message d’erreur suivant :

**Échec de conteneur de stockage toodelete « VHD ». Erreur : Il existe actuellement un bail sur le conteneur de hello et aucun ID de bail a été spécifié dans la demande hello.**

Ce problème peut se produire parce que le conteneur de hello possède un disque dur virtuel est verrouillé dans l’état du bail hello.

### <a name="scenario-3"></a>Scénario 3
Lorsque vous essayez de toodelete un compte de stockage dans un déploiement du Gestionnaire de ressources, vous recevez hello message d’erreur suivant :

**Échec de compte de stockage toodelete 'StorageAccountName'. Erreur : compte de stockage hello ne peut pas être supprimé en raison des artefacts tooits en cours d’utilisation.**

Ce problème peut se produire, car le compte de stockage hello contient un disque dur virtuel qui se trouve dans l’état du bail hello.

## <a name="solution"></a>Solution 
tooresolve ces problèmes, vous devez identifier hello VHD qui provoque l’erreur de hello et hello associé la machine virtuelle. Ensuite, détacher hello disque dur virtuel à partir de hello VM (pour les disques de données) ou supprimer hello machine virtuelle qui est à l’aide de hello disque dur virtuel (pour les disques du système d’exploitation). Cela supprime les bail hello hello disque dur virtuel et il toobe supprimé. 

toodo, utilisez une des méthodes suivantes de hello :

### <a name="method-1---use-azure-storage-explorer"></a>Méthode 1 - Utiliser l’Explorateur de stockage Azure

### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>Hello d’identifier l’étape 1 disque dur virtuel qui empêche la suppression de compte de stockage hello

1. Lorsque vous supprimez le compte de stockage hello, vous recevez une boîte de dialogue de message tels que les suivants hello : 

    ![message lors de la suppression du compte de stockage hello](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Vérifiez hello **disque URL** compte de stockage tooidentify hello et hello disque dur virtuel que vous empêche de supprimer le compte de stockage hello. Dans l’exemple suivant de hello, hello chaîne avant «. blob.core.windows.net » est le nom de compte de stockage hello et « SCCM2012-2015-08-28.vhd » est le nom du disque dur virtuel hello.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

### <a name="step-2-delete-hello-vhd-by-using-azure-storage-explorer"></a>Hello de suppression de l’étape 2 disque dur virtuel à l’aide de l’Explorateur de stockage Azure

1. Télécharger et installer la version plus récente hello de [Azure Storage Explorer](http://storageexplorer.com/). Cet outil est une application autonome de Microsoft qui vous permet de travail tooeasily avec des données de stockage Azure sur Windows, Mac OS et Linux.
2. Ouvrez l’Explorateur de stockage Azure, sélectionnez ![l’icône de compte](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/account.png) sur la barre de gauche hello, sélectionnez votre environnement Azure, puis connectez-vous.

3. Sélectionnez tous les abonnements ou abonnement hello qui contient le compte de stockage hello souhaité toodelete.

    ![ajouter un abonnement](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/addsub.png)

4. Atteindre le compte de stockage toohello que nous avons obtenu à partir de Bonjour disque URL auparavant, activez Bonjour **conteneurs d’objets Blob** > **disques durs virtuels** et recherchez hello disque dur virtuel qui vous empêche de supprimer le compte stockage hello.
5. Si hello disque dur virtuel est trouvée, vérifier hello **nom de machine virtuelle** hello toofind de colonne virtuelle qui est à l’aide de ce disque dur virtuel.

    ![Rechercher la machine virtuelle](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/check-vm.png)

6. Supprimez les bail hello hello disque dur virtuel à l’aide du portail Azure. Pour plus d’informations, consultez [bail de hello supprimer à partir de disque dur virtuel de hello](#remove-the-lease-from-the-vhd). 

7. Accédez toohello Explorateur de stockage Azure, hello disque dur virtuel d’avec le bouton droit et sélectionnez Supprimer.

8. Supprimer le compte de stockage hello.

### <a name="method-2---use-azure-portal"></a>Méthode 2 - Utiliser le portail Azure 

#### <a name="step-1-identify-hello-vhd-that-prevent-deletion-of-hello-storage-account"></a>Étape 1 : Identifier hello VHD qui empêche la suppression de compte de stockage hello

1. Lorsque vous supprimez le compte de stockage hello, vous recevez une boîte de dialogue de message tels que les suivants hello : 

    ![message lors de la suppression du compte de stockage hello](media/storage-resource-manager-cannot-delete-storage-account-container-vhd/delete-storage-error.png) 

2. Vérifiez hello **disque URL** compte de stockage tooidentify hello et hello disque dur virtuel que vous empêche de supprimer le compte de stockage hello. Dans l’exemple suivant de hello, hello chaîne avant «. blob.core.windows.net » est le nom de compte de stockage hello et « SCCM2012-2015-08-28.vhd » est le nom du disque dur virtuel hello.  

        https://portalvhds73fmhrw5xkp43.blob.core.windows.net/vhds/SCCM2012-2015-08-28.vhd

2. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
3. Dans le menu du Hub hello, sélectionnez **toutes les ressources**. Atteindre le compte de stockage toohello, puis sélectionnez **BLOB** > **disques durs virtuels**.

    ![Capture d’écran du portail hello, avec un compte de stockage hello et conteneur de « disques durs virtuels » hello mis en surbrillance](./media/storage-resource-manager-cannot-delete-storage-account-container-vhd/opencontainer.png)

4. Recherchez hello disque dur virtuel que nous avons obtenu à partir de l’URL de disque hello. Ensuite, déterminer à l’aide de la machine virtuelle hello du disque dur virtuel. En règle générale, vous pouvez déterminer qui contient les ordinateurs virtuels hello disque dur virtuel en vérifiant le nom du disque dur virtuel de hello :

Machine virtuelle dans le modèle de développement Resource Manager

   * Généralement, les disques de système d’exploitation respectent la convention d’affectation de noms suivante : NomMachineVirtuelle-AAAA-MM-JJ-HHMMSS.vhd
   * Généralement, les disques de données respectent la convention d’affectation de noms suivante : NomMachineVirtuelle-AAAA-MM-JJ-HHMMSS.vhd

Machine virtuelle dans le modèle de développement classique

   * Généralement, les disques de système d’exploitation respectent la convention d’affectation de noms suivante : NomServiceCloud-NomMachineVirtuelle-AAAA-MM-JJ-HHMMSS.vhd
   * Généralement, les disques de données respectent la convention d’affectation de noms suivante : NomServiceCloud-NomMachineVirtuelle-AAAA-MM-JJ-HHMMSS.vhd

#### <a name="step-2-remove-hello-lease-from-hello-vhd"></a>Étape 2 : Supprimer le bail de hello de hello disque dur virtuel

[Supprimez les bail hello hello VHD](#remove-the-lease-from-the-vhd), puis supprimez le compte de stockage hello.

## <a name="what-is-a-lease"></a>Qu’est-ce qu’un bail ?
Un bail est un verrou qui peut être des objets blob de tooa d’accès toocontrol utilisé (par exemple, un disque dur virtuel). Quand un objet blob est loué, seuls les propriétaires de hello du bail de hello accessible blob de hello. Un bail est important pour hello suivant raisons :

* Il empêche les données endommagées si plusieurs propriétaires essayez toowrite toohello même partie de l’objet blob de hello à hello même temps.
* Il empêche les blob hello d’être supprimé si quelque chose est activement à l’aide d’il (par exemple, une machine virtuelle).
* Il empêche le compte de stockage hello d’être supprimé si quelque chose est activement à l’aide d’il (par exemple, une machine virtuelle).

### <a name="remove-hello-lease-from-hello-vhd"></a>Supprimez les bail hello hello disque dur virtuel
Si hello disque dur virtuel est un disque de système d’exploitation, vous devez supprimer le bail de hello tooremove hello machine virtuelle :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur hello **Hub** menu, sélectionnez **virtuels**.
3. Sélectionnez hello machine virtuelle qui détient un bail sur le disque dur virtuel de hello.
4. Assurez-vous que rien n’est activement à l’aide de hello d’ordinateurs virtuels et que vous avez besoin n’est plus hello machine virtuelle.
5. En haut de hello Hello **détails de l’ordinateur virtuel** panneau, sélectionnez **supprimer**, puis cliquez sur **Oui** tooconfirm.
6. Hello machine virtuelle doit être supprimé, mais hello VHD peut être conservée. Toutefois, hello disque dur virtuel doit n’ont plus un bail sur ce dernier. Il peut prendre quelques minutes pour toobe de bail hello publié. tooverify qui hello bail est libéré, accédez trop**toutes les ressources** > **nom de compte de stockage** > **BLOB**  >  **disques durs virtuels**. Bonjour **propriétés d’objets Blob** volet, hello **état du bail** la valeur doit être **déverrouillé**.

Si hello disque dur virtuel est un disque de données, détachez hello disque dur virtuel à partir de bail de hello tooremove hello machine virtuelle :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur hello **Hub** menu, sélectionnez **virtuels**.
3. Sélectionnez hello machine virtuelle qui détient un bail sur le disque dur virtuel de hello.
4. Sélectionnez **disques** sur hello **détails de l’ordinateur virtuel** panneau.
5. Sélectionnez le disque de données hello qui détient un bail sur le disque dur virtuel de hello. Vous pouvez déterminer les VHD est attachée en disque hello en vérifiant les URL hello Hello disque dur virtuel.
6. Déterminer avec certitude que rien n’est activement à l’aide disque de données hello.
7. Cliquez sur **détachement** sur hello **disque détails** panneau.
8. disque de Hello doit maintenant être détaché hello machine virtuelle, ainsi que hello disque dur virtuel n’est plus un bail sur ce dernier. Il peut prendre quelques minutes pour toobe de bail hello publié. tooverify qui hello bail a été publié, accédez trop**toutes les ressources** > **nom de compte de stockage** > **BLOB**  >  **disques durs virtuels**. Bonjour **propriétés d’objets Blob** volet, hello **état du bail** la valeur doit être **déverrouillé**.

## <a name="next-steps"></a>Étapes suivantes
* [Suppression d'un compte de stockage](storage-create-storage-account.md#delete-a-storage-account)
* [Comment toobreak hello verrouillé le bail de stockage d’objets blob dans Microsoft Azure (PowerShell)](https://gallery.technet.microsoft.com/scriptcenter/How-to-break-the-locked-c2cd6492)
