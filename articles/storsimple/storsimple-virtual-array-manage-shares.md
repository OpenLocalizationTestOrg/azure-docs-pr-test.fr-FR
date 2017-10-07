---
title: partage de StorSimple Virtual Array aaaManage | Documents Microsoft
description: "Décrit les hello StorSimple le Gestionnaire de périphériques et explique comment toouse il partages toomanage sur votre tableau virtuel StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a>Utiliser des partages toomanage du service de gestionnaire de périphériques StorSimple hello sur hello StorSimple Virtual Array

## <a name="overview"></a>Vue d'ensemble

Ce didacticiel explique comment toouse hello toocreate du service Gestionnaire de périphériques StorSimple et gérer les partages sur votre tableau virtuel StorSimple.

Hello service du Gestionnaire de périphériques StorSimple est une extension Bonjour portail Azure qui vous permet de gérer votre solution StorSimple à partir d’une seule interface web. Dans Ajout toomanaging partages et les volumes, vous pouvez utiliser hello le Gestionnaire de périphériques StorSimple service tooview gérer les appareils, afficher les alertes, gérer les stratégies de sauvegarde et gérer le catalogue de sauvegarde hello.

## <a name="share-types"></a>Types de partages

Les partages StorSimple peuvent être les suivants :

* **Attaché localement**: les données dans ces partages reste sur le tableau de hello en permanence et ne pas déborder toohello cloud.
* **Niveaux**: les données dans ces partages peuvent déborder toohello cloud. Lorsque vous créez un partage hiérarchisé, environ 10 % d’espace de hello est approvisionné sur le niveau de local hello et 90 % d’espace de hello est configuré dans le cloud de hello. Par exemple, si vous avez configuré un partage de 1 To, 100 Go peut résider dans un espace local hello et 900 Go sera utilisée dans le cloud de hello hello lorsque des niveaux de données. À son tour, cela implique que si vous manquez tout l’espace local hello sur l’appareil de hello, vous ne pouvez pas configurer un partage hiérarchisé (car hello 10 % requis sur hello local niveau ne sera pas disponible).

### <a name="provisioned-capacity"></a>Capacité allouée

Consultez toohello tableau pour une capacité déployée maximale pour chaque type de partage suivant.

| **Identificateur de la limite** | **Limite** |
| --- | --- |
| Taille minimale d’un partage hiérarchisé |500 Go |
| Taille maximale d’un partage hiérarchisé |20 To |
| Taille minimale d'un partage épinglé localement |50 Go |
| Taille maximale d'un partage épinglé localement |2 To |

## <a name="hello-shares-blade"></a>Panneau de partages Hello

Hello **partages** menu sur votre Panneau de résumé du service StorSimple affiche la liste hello des partages de stockage sur un tableau de StorSimple donné et vous permet de toomanage les.

![Panneau Partages](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

Un partage est constitué d’une série d’attributs :

* **Nom de partage** : un nom descriptif qui doit être uniques et permet d’identifier le partage de hello.
* **État** : peut être en ligne ou hors connexion. Si un partage est hors connexion, utilisateurs du partage de hello ne seront pas en mesure de tooaccess il.
* **Type** – indique si le partage de hello est **à plusieurs niveaux** (hello par défaut) ou **attaché localement**.
* **Capacité** – spécifie la quantité hello de données utilisées comme comparés toohello la quantité totale de données qui peuvent être stockées sur le partage de hello.
* **Description** – un paramètre facultatif qui permet de décrire le partage de hello.
* **Autorisations** -hello autorisations toohello partage NTFS qui peut être géré via l’Explorateur Windows.
* **Sauvegarde** : en cas de hello StorSimple Virtual Array, tous les partages sont automatiquement activés pour sauvegarde.

![Détails des partages](./media/storsimple-virtual-array-manage-shares/share-details.png)

Suivez les instructions de hello dans cette hello didacticiel tooperform tâches suivantes :

* Ajouter un partage
* Modifier un partage
* Mettre un partage hors connexion
* Supprimer un partage

## <a name="add-a-share"></a>Ajouter un partage

1. Dans le volet Résumé du service de StorSimple hello, cliquez sur **+ ajouter partage** à partir de la barre de commandes hello. Cela ouvre hello **ajouter partage** panneau.

    ![Ajouter un partage](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. Bonjour **ajouter partage** panneau, hello suivant :
   
    1. Bonjour **nom de partage** , entrez un nom unique pour le partage. nom de Hello doit être une chaîne qui contient des caractères too127 3.

    2. Facultatif **Description** pour partage de hello. description de Hello aidera à identifier les propriétaires de partage hello.

    3. Bonjour **Type** déroulante liste, spécifiez si toocreate un **à plusieurs niveaux** ou **attaché localement** partager. Pour les charges de travail qui nécessitent des garanties locales, une faible latence et les meilleures performances possibles, sélectionnez un **Partage attaché localement**. Pour toutes les autres données, sélectionnez un partage **Hiérarchisé**.

    4. Bonjour **capacité** Indiquez la taille de hello du partage de hello. Un partage hiérarchisé doit être compris entre 500 Go et 20 To, tandis qu’un partage attaché doit être compris entre 50 Go et 2 To.

    5. Bonjour **valeur par défaut toutes les autorisations** champ, affecter hello autorisations toohello utilisateur ou groupe hello qui accède à ce partage. Spécifier le nom hello de hello utilisateur ou un groupe d’utilisateurs hello  _john@contoso.com_  format. Nous vous recommandons d’utiliser un tooaccess des privilèges d’administrateur utilisateur groupe (au lieu d’un seul utilisateur) tooallow ces partages. Une fois que vous avez affecté des autorisations hello ici, vous pouvez ensuite utiliser l’Explorateur de fichiers toomodify ces autorisations.
3. Lorsque vous avez terminé de configurer votre partage, cliquez sur **Créer**. Un partage sera créé avec hello spécifié les paramètres et que vous voyez une notification. Par défaut, la sauvegarde sera être activée pour le partage de hello.
4. tooconfirm qui hello partage a été a été créé correctement, accédez toohello **partages** panneau. Vous devez voir hello partager répertoriées.
   
    ![Le partage stimule la réussite.](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a>Modifier un partage

Modifier un partage lorsque vous avez besoin de description de hello toochange du partage de hello. Aucun autres propriétés de partage ne peuvent être modifiées une fois que le partage de hello est créé.

#### <a name="toomodify-a-share"></a>toomodify un partage

1. À partir de hello **partages** définissant panneau Résumé du service StorSimple hello, sélectionnez hello tableau virtuel sur le hello partage que vous souhaitez vous toomodify réside.
2. **Sélectionnez** hello description actuelle de partage tooview hello et le modifier.
3. Enregistrez vos modifications en cliquant sur hello **enregistrer** barre de commandes. Vos paramètres spécifiés sont appliqués ; une notification s’affiche.
   
    ![ Modifier un partage](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a>Mettre un partage hors connexion

Vous devrez peut-être tootake un partage hors connexion lors de la planification toomodify ou supprimer il. Lorsqu’un partage est hors connexion, il n’est pas disponible pour l’accès en lecture-écriture. Vous devez tootake hello partage hors connexion sur l’ordinateur hôte de hello, ainsi que sur les appareils hello.

#### <a name="tootake-a-share-offline"></a>tootake un partage hors connexion

1. Assurez-vous que ce partage hello en question n’est pas en cours d’utilisation avant sa mise hors connexion.
2. Prendre hello partage tableau hello hors connexion en effectuant hello comme suit :
   
    1. À partir de hello **partages** définissant panneau Résumé du service StorSimple hello, sélectionnez hello tableau virtuel sur le hello partage que vous souhaitez vous tootake hors connexion réside.

    2. **Sélectionnez** du partage de hello et cliquez sur **...**  (vous pouvez également cliquer avec le bouton droit dans cette ligne) et dans le menu contextuel de hello, sélectionnez **mettre hors connexion**.
     
        ![Partage hors connexion](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. Passez en revue les informations de hello Bonjour **mettre hors connexion** panneau et confirmez que vous acceptez d’opération de hello. Cliquez sur **mettre hors connexion** partage de hello tootake hors connexion. Vous voyez une notification d’opération hello en cours d’exécution.

    4. tooconfirm qui hello partage a été effectuée correctement hors connexion, accédez toohello **partages** panneau. Vous devez voir l’état hello du partage hello comme étant hors connexion.

## <a name="delete-a-share"></a>Supprimer un partage

> [!IMPORTANT]
> Un partage peut être supprimé uniquement s’il est hors connexion.


Hello complet suivant les étapes toodelete un partage.

#### <a name="toodelete-a-share"></a>toodelete un partage

1. À partir de hello **partages** définissant panneau Résumé du service StorSimple hello, sélectionnez hello tableau virtuel sur le partage hello vous souhaitez toodelete réside.
2. **Sélectionnez** du partage de hello et cliquez sur **...**  (vous pouvez également cliquer avec le bouton droit dans cette ligne) et dans le menu contextuel de hello, sélectionnez **supprimer**.
   
    ![Supprimer un partage](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. Vérifier l’état de hello du partage de hello souhaité toodelete. Si le partage hello toodelete n’est pas hors connexion, mettre hors connexion tout d’abord. Suivez les étapes de hello dans [hors connexion un partage](#take-a-share-offline).
4. Lorsque vous êtes invité à confirmer l’opération Bonjour **supprimer** panneau, acceptez la confirmation de hello et cliquez sur **supprimer**. partage de Hello va être supprimée et hello **partages** panneau affiche la liste de hello mis à jour d’actions au sein de l’unité de stockage virtuelle hello.

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment trop[cloner un partage de StorSimple](storsimple-virtual-array-clone.md).

