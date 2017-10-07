---
title: "enregistrements de contrôle d’accès aaaManage dans StorSimple | Documents Microsoft"
description: "Décrit comment le contrôle d’accès toouse enregistre toodetermine (ACR) les hôtes qui peuvent se connecter volume tooa sur l’appareil StorSimple hello."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Utiliser des enregistrements de contrôle d’accès hello StorSimple Manager service toomanage

## <a name="overview"></a>Vue d'ensemble
Enregistrements de contrôle d’accès (ACR) permettent de toospecify les hôtes qui peuvent se connecter volume tooa sur l’appareil StorSimple hello. ACR sont définies les volume spécifique tooa et contenir hello iSCSI (IQN) de noms qualifiés d’hôtes de hello. Quand un hôte tente de tooconnect tooa volume, les appareils hello vérifie hello QU'ACR associé à ce volume pour le nom IQN de hello et si une correspondance est trouvée, hello est établie. Hello des enregistrements de contrôle d’accès dans hello **Configuration** section de votre Panneau de service du Gestionnaire de périphériques StorSimple afficher tous les enregistrements de contrôle d’accès hello avec hello correspondant iqn des hôtes de hello.

Ce didacticiel explique hello suivant ACR tâches :

* Ajouter un enregistrement de contrôle d’accès
* Modifier un enregistrement de contrôle d’accès
* Supprimer un enregistrement de contrôle d’accès

> [!IMPORTANT]
> * Lorsque vous affectez un volume de tooa ACR, prenez soin que volume de hello n'est pas accédé simultanément par plus d’un hôte non cluster, car cela peut endommager le volume de hello.
> * Lorsque vous supprimez un ACR d’un volume, assurez-vous que cet hôte correspondant hello n’accède pas aux volumes de hello, car la suppression de hello pourrait entraîner une interruption en lecture-écriture.

## <a name="get-hello-iqn"></a>Obtenir hello IQN

Effectuer hello suivant les étapes tooget hello IQN d’un hôte Windows qui exécute Windows Server 2012.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a>Ajouter un enregistrement de contrôle d’accès
Vous utilisez hello **Configuration** section hello le Gestionnaire de périphériques StorSimple service panneau tooadd ACR. En général, vous associez un enregistrement de contrôle d’accès à un volume.

Effectuer hello suivant les étapes tooadd un ACR.

#### <a name="tooadd-an-acr"></a>tooadd un ACR

1. Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, double-cliquez sur service hello nom, puis dans hello **Configuration** , cliquez sur **enregistrements de contrôle d’accès**.
2. Bonjour **enregistrements de contrôle d’accès** panneau, cliquez sur **+ ajouter un ACR**.

    ![Cliquer sur Ajouter un ACR](./media/storsimple-8000-manage-acrs/createacr1.png)

3. Bonjour **ajouter un ACR** panneau, hello comme suit :

    1. Saisissez un nom pour votre ACR.
    
    2. Fournissez le nom IQN de hello de votre hôte Windows Server sous **iSCSI (IQN) de nom initiateur**.

    3. Cliquez sur **ajouter** toocreate hello ACR.

        ![Cliquer sur Ajouter un ACR](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  Hello récemment ajouté QU'ACR s’affichera dans la liste tabulaire hello d’ACR.

    ![Cliquer sur Ajouter un ACR](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a>Modifier un enregistrement de contrôle d’accès
Vous utilisez hello **Configuration** section hello le Gestionnaire de périphériques StorSimple service panneau tooedit ACR.

> [!NOTE]
> Il vous est recommandé de modifier uniquement les enregistrements de contrôle d’accès qui ne sont pas en cours d’utilisation. tooedit qu'un ACR associé à un volume qui est actuellement en cours d’utilisation, vous devez tout d’abord mettre hello volume hors connexion.

Effectuer hello suivant les étapes tooedit un ACR.

#### <a name="tooedit-an-access-control-record"></a>tooedit un enregistrement de contrôle d’accès
1.  Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, double-cliquez sur service hello nom, puis dans hello **Configuration** , cliquez sur **enregistrements de contrôle d’accès**.

    ![Accédez tooaccess des enregistrements de contrôle](./media/storsimple-8000-manage-acrs/createacr1.png)

2. Dans hello tabulaire la liste des enregistrements de contrôle d’accès hello, cliquez sur et sélectionnez hello ACR que vous souhaitez toomodify.

    ![Modifier des enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/editacr1.png)

3. Bonjour **enregistrement de contrôle d’accès modifier** panneau, fournir un autre hôte tooanother correspondant IQN.

    ![Modifier des enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/editacr2.png)

4. Cliquez sur **Enregistrer**. Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération. 

    ![Modifier des enregistrements de contrôle d’accès](./media/storsimple-8000-manage-acrs/editacr3.png)

5. Vous êtes averti lorsque hello ACR est mis à jour. la liste tabulaire Hello met également à jour les modifications de hello tooreflect.

   
## <a name="delete-an-access-control-record"></a>Supprimer un enregistrement de contrôle d’accès
Vous utilisez hello **Configuration** section hello le Gestionnaire de périphériques StorSimple service panneau toodelete ACR.

> [!NOTE]
> Vous pouvez uniquement supprimer les enregistrements de contrôle d’accès qui ne sont pas en cours d’utilisation. toodelete qu'un ACR associé à un volume qui est actuellement en cours d’utilisation, vous devez tout d’abord mettre hello volume hors connexion.

Effectuer hello suivant les étapes toodelete un enregistrement de contrôle d’accès.

#### <a name="toodelete-an-access-control-record"></a>toodelete un enregistrement de contrôle d’accès
1.  Atteindre le service du Gestionnaire de périphériques StorSimple tooyour, double-cliquez sur service hello nom, puis dans hello **Configuration** , cliquez sur **enregistrements de contrôle d’accès**.

    ![Accédez tooaccess des enregistrements de contrôle](./media/storsimple-8000-manage-acrs/createacr1.png)

2. Dans hello tabulaire la liste des enregistrements de contrôle d’accès hello, cliquez sur et sélectionnez hello ACR que vous souhaitez toodelete.

    ![Accédez tooaccess des enregistrements de contrôle](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. Menu contextuel de hello tooinvoke et sélectionnez **supprimer**.

    ![Accédez tooaccess des enregistrements de contrôle](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. Lorsque vous êtes invité à confirmer l’opération, passez en revue les informations hello et puis cliquez sur **supprimer**.

    ![Accédez tooaccess des enregistrements de contrôle](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. Vous êtes averti lorsque la suppression hello est terminée. la liste tabulaire Hello est mise à jour tooreflect hello suppression.

    ![Accédez tooaccess des enregistrements de contrôle](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur la [gestion des volumes StorSimple](storsimple-8000-manage-volumes-u2.md).
* En savoir plus sur [à l’aide de hello tooadminister du service StorSimple Manager votre appareil StorSimple](storsimple-8000-manager-service-administration.md).

