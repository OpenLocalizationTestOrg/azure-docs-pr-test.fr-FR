---
title: "enregistrements de contrôle d’accès aaaManage pour StorSimple Virtual Array | Documents Microsoft"
description: "Décrit comment le contrôle d’accès toomanage enregistre toodetermine (ACR) les hôtes qui peuvent se connecter tooa volume hello StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a>Utilisez le Gestionnaire de périphérique StorSimple toomanage des enregistrements de contrôle d’accès pour StorSimple Virtual Array

## <a name="overview"></a>Vue d'ensemble

Enregistrements de contrôle d’accès (ACR) permettent de toospecify les hôtes qui peuvent se connecter tooa volume hello StorSimple Virtual Array (également appelé hello local périphérique virtuel StorSimple). ACR sont définies les volume spécifique tooa et contenir hello iSCSI (IQN) de noms qualifiés d’hôtes de hello. Quand un hôte tente de tooconnect tooa volume, les appareils hello vérifie hello ACR associé à ce volume pour le nom IQN de hello, et s’il existe une correspondance, puis hello est établie. Hello **enregistrements de contrôle d’accès** panneau dans hello **Configuration** section de votre service de gestionnaire de périphériques affiche tous les enregistrements de contrôle d’accès hello avec hello correspondant iqn des hôtes de hello.

![Gestion d’enregistrements de contrôle d’accès](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

Ce didacticiel explique hello suivant ACR tâches :

* Obtenir hello IQN
* Ajouter un enregistrement de contrôle d’accès
* Modifier un enregistrement de contrôle d’accès
* Supprimer un enregistrement de contrôle d’accès

> [!IMPORTANT]
> 
> * Lorsque vous affectez un volume de tooa ACR, prenez soin que volume de hello n'est pas accédé simultanément par plus d’un hôte non cluster, car cela peut endommager le volume de hello.
> * Lorsque vous supprimez un ACR d’un volume, assurez-vous que cet hôte correspondant hello n’accède pas aux volumes de hello, car la suppression de hello pourrait entraîner une interruption en lecture-écriture.


## <a name="get-hello-iqn"></a>Obtenir hello IQN

Effectuer hello suivant les étapes tooget hello IQN d’un hôte Windows qui exécute Windows Server 2012.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a>Ajouter un enregistrement de contrôle d’accès

Vous utilisez **enregistrements de contrôle d’accès** panneau dans hello **Configuration** section de votre tooadd de service du Gestionnaire de périphériques StorSimple ACR. En général, vous associez un enregistrement de contrôle d’accès à un volume.

Pour plus d’informations sur l’association d’un ACR à un volume, accédez trop[ajouter un volume](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

> [!IMPORTANT]
> Lorsque vous affectez un volume de tooa ACR, prenez soin que volume de hello n'est pas accédé simultanément par plus d’un hôte non cluster, car cela peut endommager le volume de hello.


Effectuer hello suivant les étapes tooadd un ACR.

#### <a name="tooadd-an-acr"></a>tooadd un ACR

1. Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur service hello nom, puis dans hello **Configuration** , cliquez sur **enregistrements de contrôle d’accès**.
2. Bonjour **enregistrements de contrôle d’accès** panneau, cliquez sur **ajouter**.
3. Bonjour **ajouter un ACR** panneau, hello suivant :
   
    1. Saisissez un **Nom** pour votre ACR.
    
    2. Sous **nom de l’initiateur iSCSI**, fournissez le nom IQN de hello de votre hôte Windows. tooget hello IQN de votre hôte Windows Server, procédez comme hello suivant :
   
    3. Démarrez l’initiateur iSCSI Microsoft hello sur votre hôte Windows. Dans la fenêtre Propriétés de l’initiateur iSCSI hello, sur hello **Configuration** , sélectionnez et copiez les chaîne hello de hello **nom de l’initiateur** champ.
    Collez cette chaîne Bonjour **IQN** champ hello **ajouter un ACR** panneau.
   
    6. Cliquez sur **ajouter** tooadd hello ACR.  
   
        ![Ajouter des enregistrements de contrôle d’accès](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. Hello Liste tabulaire est mis à jour tooreflect cet ajout.

## <a name="edit-an-acr"></a>Modifier un enregistrement de contrôle d’accès

Vous utilisez hello **enregistrements de contrôle d’accès** panneau dans hello **Configuration** section de votre service de gestionnaire de périphériques Bonjour Azure tooedit portail ACR.

> [!NOTE]
> Vous ne devez pas modifier un enregistrement de contrôle d’accès en cours d’utilisation. tooedit qu'un ACR associé à un volume qui est actuellement en cours d’utilisation, vous devez tout d’abord mettre hello volume hors connexion.


Effectuer hello suivant les étapes tooedit un ACR.

#### <a name="tooedit-an-acr"></a>tooedit un ACR

1. Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur service hello nom, puis dans hello **Configuration** section, **enregistrements de contrôle d’accès**.
2. Bonjour **enregistrements de contrôle d’accès** panneau, à partir de la liste tabulaire hello des enregistrements de contrôle d’accès hello, double-cliquez sur hello ACR que vous souhaitez toomodify.
3. Bonjour **enregistrements de contrôle d’accès modifier** panneau, hello suivant :
   
    1. Approvisionnement hello IQN pour hello ACR.
   
    2. Cliquez sur **enregistrer** haut hello hello panneau toosave hello modifié ACR. Vous consultez hello message de confirmation suivant :
   
        ![Modifier des enregistrements de contrôle d’accès](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a>Supprimer un enregistrement de contrôle d’accès

Vous utilisez hello **Configuration** page Bonjour Azure toodelete portail ACR.

> [!NOTE]
> 
> * Vous ne devez pas supprimer un enregistrement de contrôle d’accès en cours d’utilisation. toodelete qu'un ACR associé à un volume qui est actuellement en cours d’utilisation, vous devez tout d’abord mettre hello volume hors connexion.
> * Lorsque vous supprimez un ACR d’un volume, assurez-vous que cet hôte correspondant hello n’accède pas aux volumes de hello, car la suppression de hello pourrait entraîner une interruption en lecture-écriture.


Effectuer hello suivant les étapes toodelete un enregistrement de contrôle d’accès.

#### <a name="toodelete-an-access-control-record"></a>toodelete un enregistrement de contrôle d’accès

1. Sur la page d’accueil hello service, sélectionnez votre service, double-cliquez sur service hello nom, puis dans hello **Configuration** section, **enregistrements de contrôle d’accès**.

2. Bonjour **enregistrements de contrôle d’accès** panneau, à partir de la liste tabulaire hello des enregistrements de contrôle d’accès hello, double-cliquez sur hello ACR que vous souhaitez toodelete.

3. Dans Panneau d’enregistrements hello modifier accès contrôle, cliquez sur **supprimer**.
   
    ![Supprimer des enregistrements de contrôle d’accès](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. Lorsque vous êtes invité à confirmer l’opération, cliquez sur **supprimer** toocontinue avec suppression des hello. la liste tabulaire Hello est mise à jour tooreflect hello suppression.
   
   ![Message d'avertissement](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a>Étapes suivantes

* Découvrez comment [ajouter des volumes et configurer les enregistrements de contrôle d’accès](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

