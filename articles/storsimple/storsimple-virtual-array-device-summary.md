---
title: "panneau Résumé du périphérique virtuel tableau aaaStorSimple | Documents Microsoft"
description: "Décrit le panneau Résumé du périphérique hello pour le Gestionnaire de périphériques StorSimple et explique comment toouse il intégrité hello toomonitor votre StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 3649eaac8a924a772f310a809ddf9706e912157a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-blade-for-storsimple-device-manager-connected-toostorsimple-virtual-array"></a>Panneau Résumé utilisation hello périphérique pour le Gestionnaire de périphériques StorSimple connecté tooStorSimple tableau virtuel

## <a name="overview"></a>Vue d'ensemble

Panneau de périphérique StorSimple le Gestionnaire de périphériques Hello fournit un résumé d’un tableau virtuel StorSimple qui est inscrit avec une donnée StorSimple Gestionnaire de périphériques, mise en évidence les problèmes de périphériques qui nécessitent une intervention d’un administrateur système. Ce didacticiel présente panneau Résumé du périphérique hello, explique la fonction et le contenu de hello et décrit les tâches hello que vous pouvez effectuer à partir de ce panneau.

panneau Résumé du périphérique Hello affiche hello informations suivantes :

![Page du tableau de bord d’un appareil](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a>Gestion

Dans le panneau de périphérique StorSimple hello, vous voyez les options hello gestion de votre périphérique StorSimple. Vous consultez les commandes de gestion hello haut hello du Panneau de hello et sur le côté gauche de hello. Utilisez ces options tooadd partages ou des volumes, ou mettre à jour ou basculer votre tableau virtuel.

Hello zone d’essentials capture certaines des propriétés importantes de hello, telles que, état de hello, modèle, version du logiciel ainsi qu’un toohello lien **l’interface utilisateur Web** du tableau de hello. Si vous êtes sur un réseau interne, vous pouvez exécuter directement hello [interface utilisateur web locale](storsimple-ova-web-ui-admin.md) tooadminister votre tableau virtuel.

![Éléments principaux des appareils](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a>Synthèse des appareils StorSimple

* Hello **alertes** vignette fournit un instantané de toutes les alertes actives hello pour votre groupe virtuel, regroupée par gravité. Cliquez sur Bonjour vignette tooopen Bonjour **alertes** panneau, puis cliquez sur un individu alerte tooview supplémentaire plus d’informations sur cette alerte, y compris les actions recommandées. Vous pouvez également effacer les alerte hello si hello est résolu.

* Hello **capacité** vignette affiche hello stockage principal qui est configuré et restants dans hello périphérique virtuel relatif toohello stockage total disponible pour hello identiques. **Configuré** fait référence toohello quantité de stockage qui est préparée et allouée à l’utilisation, **restant** fait référence toohello restant de capacité qui peut être configurée sur ce périphérique. Hello **hiérarchisé restantes** capacité est la capacité disponible hello qui peut être configurée, y compris le nuage, tout en hello **restant Local** est la capacité hello restant sur des disques hello attaché toothis virtuel tableau.

* Bonjour **utilisation** graphique, vous pouvez afficher les stockage principal hello utilisé dans votre tableau virtuel, ainsi que les stockages hello consommées sur hello des 7 derniers jours, la valeur par défaut de hello laps de temps. Hello d’utilisation **modifier** option hello en haut à droite de hello graphique toochoose une échelle de temps différent.

* Hello **partages** ou **Volumes** vignette fournit un résumé du nombre de hello de partages ou volumes de votre appareil, regroupés par état. Cliquez sur Bonjour vignette tooopen Bonjour **partages** ou **Volumes** liste panneau, puis cliquez sur une tooview partage ou volume individuel ou modifier ses propriétés. Pour plus d’informations, consultez Comment trop[gérer les partages](storsimple-virtual-array-manage-shares.md) ou [gérer les volumes](storsimple-virtual-array-manage-volumes.md).

## <a name="next-steps"></a>Étapes suivantes
Découvrez comment :
- [Gérer des partages sur une instance StorSimple Virtual Array](storsimple-virtual-array-manage-shares.md)
    
- [Gérer des volumes sur une instance StorSimple Virtual Array](storsimple-virtual-array-manage-volumes.md)

