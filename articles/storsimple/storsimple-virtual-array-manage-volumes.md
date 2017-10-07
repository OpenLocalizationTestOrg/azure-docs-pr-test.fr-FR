---
title: volumes StorSimple Virtual Array aaaManage | Documents Microsoft
description: "Décrit les hello StorSimple le Gestionnaire de périphériques et explique comment toouse il toomanage des volumes sur votre tableau virtuel StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a>Utilisez le Gestionnaire de périphériques StorSimple volumes de toomanage service sur hello StorSimple Virtual Array

## <a name="overview"></a>Vue d'ensemble

Ce didacticiel explique comment toouse hello toocreate du service Gestionnaire de périphériques StorSimple et gestion des volumes sur votre tableau virtuel StorSimple.

Hello service du Gestionnaire de périphériques StorSimple est une extension Bonjour portail Azure qui vous permet de gérer votre solution StorSimple à partir d’une seule interface web. Dans Ajout toomanaging partages et les volumes, vous pouvez utiliser tooview de service de gestionnaire de périphériques StorSimple hello et gérer les appareils, afficher les alertes et afficher et gérer les stratégies de sauvegarde et de catalogue de sauvegarde hello.

## <a name="volume-types"></a>Types de volume

Les volumes StorSimple peuvent être les suivants :

* **Attaché localement**: données de ces volumes reste sur le tableau de hello en permanence et ne pas déborder toohello cloud.
* **Niveaux**: données de ces volumes peuvent déborder toohello cloud. Lorsque vous créez un volume hiérarchisé, environ 10 % d’espace de hello est approvisionné sur le niveau de local hello et 90 % d’espace de hello est configuré dans le cloud de hello. Par exemple, si vous avez configuré un volume de 1 To, 100 Go peut résider dans un espace local hello et 900 Go sera utilisée dans le cloud de hello hello lorsque des niveaux de données. À son tour, cela implique que si vous manquez tout l’espace local hello sur l’appareil de hello, vous ne pouvez pas configurer un volume hiérarchisé (car hello 10 % requis sur hello local niveau ne sera pas disponible).

### <a name="provisioned-capacity"></a>Capacité allouée
Consultez toohello tableau pour une capacité déployée maximale pour chaque type de volume.

| **Identificateur de la limite**                                       | **Limite**     |
|------------------------------------------------------------|---------------|
| Taille minimale d’un volume hiérarchisé                            | 500 Go        |
| Taille maximale d’un volume hiérarchisé                            | 5 To          |
| Taille minimale d'un volume épinglé localement                    | 50 Go         |
| Taille maximale d'un volume épinglé localement                    | 500 Go        |

## <a name="hello-volumes-blade"></a>Panneau de Volumes Hello
Hello **Volumes** menu sur votre Panneau de résumé du service StorSimple affiche la liste hello des volumes de stockage sur un tableau de StorSimple donné et vous permet de toomanage les.

![Panneau Volumes](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

Un volume est constitué d’une série d’attributs :

* **Nom de volume** – un nom descriptif qui doit être uniques et permet d’identifier le volume de hello.
* **État** : peut être en ligne ou hors connexion. Si un volume est hors connexion, il n’est pas visible tooinitiators (serveurs) autorisés accès toouse hello volume.
* **Type** – indique si le volume de hello est **à plusieurs niveaux** (hello par défaut) ou **attaché localement**.
* **Capacité** – spécifie la quantité hello de données utilisées comme comparés toohello la quantité totale de données qui peuvent être stockées à l’initiateur hello (serveur).
* **Sauvegarde** : en cas de hello StorSimple Virtual Array, tous les volumes sont automatiquement activés pour sauvegarde.
* **Connecté des ordinateurs hôtes** – spécifie les initiateurs hello (serveurs) autorisés accès toothis volume.

![Détails de volumes](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

Suivez les instructions de hello dans cette hello didacticiel tooperform tâches suivantes :

* Ajout d’un volume
* Modification d’un volume
* Mise hors connexion d’un volume
* Suppression d’un volume

## <a name="add-a-volume"></a>Ajout d’un volume

1. Dans le volet Résumé du service de StorSimple hello, cliquez sur **+ ajouter un volume** à partir de la barre de commandes hello. Cela ouvre hello **Ajout du volume** panneau.
   
    ![Ajouter un volume](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. Bonjour **Ajout du volume** panneau, hello suivant :
   
   * Bonjour **nom de Volume** , entrez un nom unique pour votre volume. nom de Hello doit être une chaîne qui contient des caractères too127 3.
   * Bonjour **Type** déroulante liste, spécifiez si toocreate un **à plusieurs niveaux** ou **attaché localement** volume. Pour les charges de travail qui nécessitent des garanties locales, une faible latence et les meilleures performances possibles, sélectionnez **Volume attaché localement**. Pour toutes les autres données, sélectionnez le volume **hiérarchisé**.
   * Bonjour **capacité** Indiquez la taille de hello du volume de hello. Un volume hiérarchisé doit être compris entre 500 Go et 5 To, tandis qu’un volume attaché doit être compris entre 50 Go et 500 Go.
   * * Cliquez sur **connecté des ordinateurs hôtes**, sélectionnez un accès contrôle enregistrement (ACR) correspondante toohello initiateur iSCSI que vous souhaitez tooconnect toothis volume, puis cliquez sur **sélectionnez**.
3. tooadd un nouvel hôte connecté, cliquez sur **ajouter un nouveau**, entrez un nom pour l’hôte de hello et son iSCSI nom qualifié (IQN), puis cliquez sur **ajouter**.
   
    ![Ajouter un volume](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. Lorsque vous avez terminé de configurer votre volume, cliquez sur **Créer**. Un volume est créé par hello spécifié settings et une notification s’affiche sur la création réussie du hello hello identiques. Par défaut, la sauvegarde sera être activée pour le volume de hello.
5. tooconfirm qui hello volume a été a été créé correctement, accédez toohello **Volumes** panneau. Vous devez voir volume hello répertorié.
   
    ![Le volume stimule la réussite](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a>Modification d’un volume

Modifier un volume lorsque vous avez besoin d’hôtes hello toochange qui accèdent aux volumes de hello. Hello autres attributs d’un volume ne peut pas être modifiées une fois que le volume de hello a été créé.

#### <a name="toomodify-a-volume"></a>toomodify un volume

1. À partir de hello **Volumes** définissant panneau Résumé du service StorSimple hello, sélectionnez hello tableau virtuel sur le hello volume que vous souhaitez vous toomodify réside.
2. **Sélectionnez** hello volume et cliquez sur **connecté des ordinateurs hôtes** tooview hello hôte actuellement connecté et modifiez-le tooa un autre serveur.
   
    ![Modifier le volume](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. Enregistrez vos modifications en cliquant sur hello **enregistrer** barre de commandes. Vos paramètres spécifiés sont appliqués ; une notification s’affiche.

## <a name="take-a-volume-offline"></a>Mise hors connexion d’un volume

Vous devrez peut-être tootake un volume hors connexion lors de la planification toomodify ou supprimer il. Lorsqu’un volume est hors connexion, il n’est pas disponible pour l’accès en lecture-écriture. Vous devez tootake hello volume hors connexion sur l’ordinateur hôte de hello, ainsi que sur les appareils hello.

#### <a name="tootake-a-volume-offline"></a>tootake un volume hors connexion

1. Assurez-vous que le volume hello en question n’est pas utilisé avant de mettre hors connexion.
2. Mettez d’abord volume hello hors connexion sur l’ordinateur hôte de hello. Cela élimine tout risque potentiel de corruption des données sur le volume de hello. Pour connaître la procédure, consultez instructions toohello de votre système d’exploitation hôte.
3. Une fois le volume hello sur l’ordinateur hôte de hello est hors connexion, prendre les volume hello tableau hello hors connexion en effectuant hello comme suit :
   
   * À partir de hello **Volumes** définissant panneau Résumé du service StorSimple hello, sélectionnez hello tableau virtuel sur le hello volume que vous souhaitez vous tootake hors connexion réside.
   * **Sélectionnez** hello volume et cliquez sur **...**  (vous pouvez également cliquer avec le bouton droit dans cette ligne) et dans le menu contextuel de hello, sélectionnez **mettre hors connexion**.
     
        ![Volume hors connexion](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * Passez en revue les informations de hello Bonjour **mettre hors connexion** panneau et confirmez que vous acceptez d’opération de hello. Cliquez sur **mettre hors connexion** tootake le volume hello hors connexion. Vous voyez une notification d’opération hello en cours d’exécution.
   * tooconfirm hello volume a été correctement mis hors connexion, accédez à toohello **Volumes** panneau. Vous devez normalement voir État hello du volume de hello hors connexion.
     
       ![Confirmation du volume hors connexion](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a>Suppression d’un volume

> [!IMPORTANT]
> Vous pouvez supprimer un volume uniquement s’il est hors connexion.
> 
> 

Terminer hello suivant les étapes toodelete un volume.

#### <a name="toodelete-a-volume"></a>toodelete un volume

1. À partir de hello **Volumes** définissant panneau Résumé du service StorSimple hello, sélectionnez hello tableau virtuel sur le hello volume que vous souhaitez vous toodelete réside.
2. **Sélectionnez** hello volume et cliquez sur **...**  (vous pouvez également cliquer avec le bouton droit dans cette ligne) et dans le menu contextuel de hello, sélectionnez **supprimer**.
   
    ![Supprimer un volume](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. Vérifier l’état de hello du volume de hello souhaité toodelete. Si hello volume de toodelete n’est pas hors connexion, des étapes il hello hors connexion de tout d’abord, suivant [mettre un volume hors connexion](#take-a-volume-offline).
4. Lorsque vous êtes invité à confirmer l’opération Bonjour **supprimer** panneau, acceptez la confirmation de hello et cliquez sur **supprimer**. volume de Hello va être supprimée et hello **Volumes** panneau affichera la liste hello mis à jour de volumes au sein de l’unité de stockage virtuelle hello.

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment trop[cloner un volume StorSimple](storsimple-virtual-array-clone.md).

