---
title: "aaaDeactivate et supprimer une unité de stockage de Microsoft Azure StorSimple virtuelle | Documents Microsoft"
description: "Décrit comment l’appareil StorSimple tooremove service en désactiver tout d’abord, puis leur suppression."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a>Désactiver et supprimer un StorSimple Virtual Array

## <a name="overview"></a>Vue d'ensemble

Lorsque vous désactivez un StorSimple Virtual Array, vous rompez connexion hello entre l’appareil de hello et le service de gestionnaire de périphériques StorSimple hello correspondant. Ce didacticiel explique comment :

* Désactiver un appareil 
* Supprimer un appareil désactivé

les informations de Hello dans cet article s’appliquent tooStorSimple tableaux virtuels uniquement. Pour plus d’informations sur la 8000 série, accédez toohow trop[désactiver ou supprimer un périphérique](storsimple-deactivate-and-delete-device.md).

## <a name="when-toodeactivate"></a>Lorsque toodeactivate ?

La désactivation est une opération DÉFINITIVE et ne peut pas être annulée. Vous ne peut pas inscrire un appareil désactivé avec hello service du Gestionnaire de périphériques StorSimple à nouveau. Vous pouvez peut-être toodeactivate et supprimer un groupe virtuel StorSimple Bonjour les scénarios suivants :

* **Le basculement planifié** : votre appareil est en ligne et que vous envisagez toofail sur votre appareil. Si vous envisagez de périphérique de tooupgrade tooa plus important, vous devrez peut-être toofail sur votre appareil. Une fois que la propriété des données hello est transférée et hello de basculement est terminé, hello source appareil est automatiquement supprimé.
* **Basculement non planifié** : votre appareil est hors connexion et que vous devez toofail via un périphérique de hello. Ce scénario peut se produire lors d’un incident lorsqu’il existe une panne dans le centre de données hello et votre appareil principal est arrêté. Vous envisagez de toofail sur hello tooa secondaire un périphérique. Une fois que la propriété des données hello est transférée et hello de basculement est terminé, hello source appareil est automatiquement supprimé.
* **Mettre hors service** : vous voulez toodecommission hello périphérique. Vous devez toofirst désactiver hello appareil, puis supprimez-le. Si vous désactivez un appareil, il n’est plus possible d’accéder aux données stockées en local. Vous pouvez uniquement l’accès et restauration hello des données stockées dans le cloud de hello. Si vous envisagez de données de l’appareil tookeep hello après la désactivation, vous devez prendre un instantané cloud de toutes vos données avant de désactiver un périphérique. Cet instantané cloud vous permet de toorecover tous hello des données à un stade ultérieur.

## <a name="deactivate-a-device"></a>Désactiver un appareil

toodeactivate votre appareil, effectuer hello comme suit.

#### <a name="toodeactivate-hello-device"></a>Appareil de hello toodeactivate

1. Dans votre service, passez trop**Gestion > appareils**. Bonjour **périphériques** panneau, cliquez sur Sélectionnez hello périphériques et que vous souhaitez toodeactivate.
   
    ![Sélectionnez le périphérique toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. Dans votre **tableau de bord périphérique** panneau, cliquez sur **... Plus** et dans la liste hello, sélectionnez **Deactivate**.
   
    ![Clic sur Désactiver](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. Bonjour **Deactivate** panneau, le nom de périphérique de type hello et puis cliquez sur **Deactivate**. 
   
    ![Confirmation de la désactivation](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    Hello désactiver le processus démarre et prend quelques minutes toocomplete.
   
    ![Désactivation en cours](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. Après la désactivation, la liste des appareils hello actualise.
   
    ![Désactivation terminée](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    Vous pouvez maintenant supprimer cet appareil.

## <a name="delete-hello-device"></a>Supprimer l’appareil de hello

Un périphérique a toodelete de désactivés premier toobe il. Suppression d’un appareil supprime de la liste hello des périphériques connectés toohello service. service de Hello puis ne peut plus gérer les appareils hello supprimé. données Hello associées hello appareil restent cependant dans le cloud de hello. Ensuite, les frais associés aux données s’accumulent.

Appareil de hello toodelete, effectuer hello comme suit.

#### <a name="toodelete-hello-device"></a>Appareil de hello toodelete

1. Dans le Gestionnaire de périphériques StorSimple, accédez trop**Gestion > appareils**. Bonjour **périphériques** panneau, sélectionnez un appareil désactivé que vous souhaitez toodelete.
2. Bonjour **tableau de bord périphérique** panneau, cliquez sur **... Plus** puis cliquez sur **supprimer**.
   
   ![Sélectionnez le périphérique toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. Bonjour **supprimer** panneau, entrez un nom hello de suppression d’un périphérique tooconfirm hello votre puis cliquez sur **supprimer**. Appareil de hello suppression ne supprime pas les données de cloud de hello associées hello périphérique. 
   
   ![Confirmation de suppression](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. suppression de Hello démarre et prend quelques minutes toocomplete.
   
   ![Suppression en cours](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    Après la suppression des appareils de hello, vous pouvez afficher la liste des appareils hello mis à jour.

## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur la façon de toofail, accédez trop[basculement et récupération d’urgence de votre tableau virtuel StorSimple](storsimple-virtual-array-failover-dr.md).

* toolearn savoir plus sur comment toouse hello service du Gestionnaire de périphériques StorSimple, accédez trop[utilisez hello tooadminister du service Gestionnaire de périphériques StorSimple votre StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md). 

