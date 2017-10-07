---
title: aaaDeactivate et supprimer un appareil StorSimple | Documents Microsoft
description: "Décrit comment l’appareil StorSimple tooremove service en désactiver tout d’abord, puis leur suppression."
services: storsimple
documentationcenter: 
author: SharS
manager: timlt
editor: 
ms.assetid: 155cda38-c5ae-45dc-b7e8-6444494afc9e
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed86bcd089aa957128e14b1709c836d938c131a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-8000-series-device-via-storsimple-manager-service"></a>Désactivation et suppression d’un appareil StorSimple série 8000 via le service StorSimple Manager
## <a name="overview"></a>Vue d'ensemble
Vous souhaiterez peut-être tootake un appareil StorSimple hors service (par exemple, si vous remplacez ou la mise à niveau de votre appareil ou si vous n’utilisez plus StorSimple). Si c’est le cas de hello, vous devez appareil de hello toodeactivate avant de pouvoir le supprimer. La désactivation d’interrompt la connexion de hello entre l’appareil de hello et le service StorSimple Manager correspondant hello. Ce didacticiel explique comment tooremove un appareil StorSimple à partir de service par tout d’abord le désactiver, puis leur suppression. 

Lorsque vous désactivez un périphérique, toutes les données stockées localement sur l’appareil de hello ne seront plus accessibles. Uniquement les données de hello associées hello périphérique qui a été enregistrée dans le cloud de hello peuvent être récupérées.  

> [!WARNING]
> La désactivation est une opération DÉFINITIVE et ne peut pas être annulée. Un appareil désactivé ne peut pas être inscrit avec le service StorSimple Manager hello sauf s’il est tout d’abord rétablir les paramètres d’usine par défaut toohello. 
> 
> Hello réinitialisation processus supprime toutes les données hello qui a été stockées localement sur votre appareil. Par conséquent, il est essentiel de prendre un instantané cloud de toutes vos données avant de désactiver un appareil. Cela vous permettra de toorecover tous hello des données à un stade ultérieur.
> 
> 

Ce didacticiel explique comment :

* Désactiver un appareil et de supprimer des données de hello
* Désactiver un appareil et conserver les données de hello

Il explique également comment fonctionnent la désactivation et la suppression sur un appareil virtuel StorSimple.

> [!NOTE]
> Avant de désactiver un périphérique physique ou virtuel de StorSimple, assurez-vous que toostop ou supprimer des clients et les hôtes qui dépendent de cet appareil.
> 
> 

## <a name="deactivate-and-delete-data"></a>Désactiver et supprimer des données
Si vous souhaitez supprimer complètement de périphérique de hello et que vous ne souhaitez pas que les données de salutation tooretain sur l’appareil de hello, puis terminez hello comme suit.

#### <a name="toodeactivate-hello-device-and-delete-hello-data"></a>toodeactivate hello dispositif et supprimer les données de salutation
1. Toodeactivating préalable un appareil, vous devez supprimer tous les hello volume conteneurs (et les volumes hello) associé au périphérique de hello. Vous pouvez supprimer des conteneurs de volumes uniquement après avoir supprimé les sauvegardes hello associé.
2. Désactiver le dispositif de hello comme suit :
   
   1. Sur hello service StorSimple Manager **périphériques** page, l’appareil de hello select que vous souhaitez toodeactivate, au bas de hello de page de hello, cliquez sur **Deactivate**.
   2. Un message de confirmation s’affiche. Cliquez sur **Oui** toocontinue. Hello désactiver le processus démarre et prendre quelques minutes toocomplete.
3. Après la désactivation, vous pouvez supprimer complètement le périphérique de hello. Suppression d’un appareil supprime de la liste hello des périphériques connectés toohello service. service de Hello puis ne peut plus gérer les appareils hello supprimé. Utilisez hello suivant l’appareil de hello toodelete comme suit :
   
   1. Sur hello service StorSimple Manager **périphériques** , sélectionnez un appareil désactivé que vous souhaitez toodelete.
   2. Bas hello sur la page de hello, cliquez sur **supprimer**.
   3. Vous êtes invité à confirmer l’opération. Cliquez sur **Oui** toocontinue.
      
      Il peut prendre quelques minutes pour hello appareil toobe est supprimé.

## <a name="deactivate-and-retain-data"></a>Désactiver et conserver des données
Si vous intéressent supprimer hello appareil mais les données de salutation tooretain, puis terminez hello comme suit.

#### <a name="toodeactivate-a-device-and-retain-hello-data"></a>toodeactivate un appareil et conserver les données de hello
1. Désactiver le dispositif de hello. Tous les hello conteneurs de volumes et instantanés hello du périphérique de hello reste.
   
   1. Sur hello service StorSimple Manager **périphériques** page, l’appareil de hello select que vous souhaitez toodeactivate, au bas de hello de page de hello, cliquez sur **Deactivate**.
   2. Un message de confirmation s’affiche. Cliquez sur **Oui** toocontinue. Hello désactiver le processus démarre et prendre quelques minutes toocomplete.
2. Vous pouvez maintenant basculer les conteneurs de volumes hello et les instantanés de hello associé. Pour les procédures, passez trop[basculement et récupération d’urgence pour votre appareil StorSimple](storsimple-device-failover-disaster-recovery.md).
3. Après la désactivation et de basculement, vous pouvez supprimer les périphériques hello complètement. Suppression d’un appareil supprime de la liste hello des périphériques connectés toohello service. service de Hello puis ne peut plus gérer les appareils hello supprimé. Hello complet suivant l’appareil de hello toodelete comme suit :
   
   1. Sur hello service StorSimple Manager **périphériques** , sélectionnez un appareil désactivé que vous souhaitez toodelete.
   2. Bas hello sur la page de hello, cliquez sur **supprimer**.
   3. Vous êtes invité à confirmer l’opération. Cliquez sur **Oui** toocontinue.
      
      Il peut prendre quelques minutes pour hello appareil toobe est supprimé.

## <a name="deactivate-and-delete-a-virtual-device"></a>Désactiver et supprimer un appareil virtuel
Pour un périphérique virtuel StorSimple, désactivation désalloue hello virtual machine. Vous pouvez ensuite supprimer la machine virtuelle de hello et ressources hello créés lors de sa préparation. Une fois un appareil virtuel hello est désactivé, il ne peut pas être restauré tooits l’état précédent. 

Résultats de la désactivation Bonjour suivant des actions :

* un appareil virtuel StorSimple Hello est supprimé.
* Hello OSDisk et des disques de données créé pour un appareil virtuel StorSimple hello sont supprimés.
* Hello Service hébergé et un réseau virtuel qui ont été créés lors de la configuration sont conservés. Si vous n’utilisez pas ces entités, vous devez les supprimer manuellement.
* Les instantanés cloud créés par un appareil virtuel StorSimple hello sont conservés.

## <a name="next-steps"></a>Étapes suivantes
* toorestore hello des valeurs par défaut de toofactory appareil désactivé, accédez trop[rétablir les paramètres par défaut de hello appareil toofactory](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).
* Pour obtenir une assistance technique, [contactez le support technique de Microsoft](storsimple-contact-microsoft-support.md).
* toolearn savoir plus sur comment toouse hello service StorSimple Manager, accédez trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md). 

