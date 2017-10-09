---
title: tableau de bord de service aaaStorSimple Manager | Documents Microsoft
description: "Décrit le tableau de bord de service hello StorSimple Manager et explique comment toouse il contrôle d’intégrité de hello toomonitor de votre solution StorSimple."
services: storsimple
documentationcenter: 
author: SharS
manager: carmonm
editor: 
ms.assetid: fb0f131d-d60b-45d7-ace2-56d0502e6627
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: dc1197eb5deac337215b260845631a4f04be1011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-dashboard"></a>Utilisez le tableau de bord de service hello StorSimple Manager
## <a name="overview"></a>Vue d'ensemble
page de tableau de bord du service StorSimple Manager Hello fournit un résumé de tous les périphériques hello qui sont connecté toohello service StorSimple Manager, mise en surbrillance ceux qui nécessitent une intervention d’un administrateur système. Ce didacticiel présente la page du tableau de bord hello, explique la fonction et le contenu du tableau de bord hello et décrit les tâches hello que vous pouvez effectuer à partir de cette page.

![Tableau de bord du service](./media/storsimple-service-dashboard/HCS_ServiceDashboard.png)

tableau de bord de service Hello StorSimple Manager affiche hello informations suivantes :

* Bonjour **graphique** zone, vous pouvez voir les mesures appropriées hello du graphique pour vos appareils. Vous pouvez afficher le stockage principal de hello (localement épinglés et à plusieurs niveaux) utilisée sur tous les périphériques de hello, ainsi que les stockages hello consommée par les périphériques sur une période de temps. Utilisez les contrôles de hello en hello en haut à droite du graphique de hello toospecify une échelle de temps de 1 semaine, 1 mois, 3 mois ou 1 an.
* Hello **présentation de l’utilisation** affiche hello stockage principal est déployé et consommé par tous les appareils toohello relatif stockage total disponible sur tous les appareils. **Configuré** fait référence toohello quantité de stockage qui est préparée et allouée à l’utilisation, tandis que **utilisé** fait référence toousage de volumes, tel qu’affiché par les initiateurs hello les périphériques connectés toohello.
* Hello **alertes** zone fournit un instantané de toutes les alertes actives hello sur tous les périphériques de hello, regroupées par gravité. Cliquez sur un niveau de gravité hello ouvre hello **alertes** page, tooshow étendue ces alertes. Sur hello **alertes** page, vous pouvez cliquer sur une tooview alerte individuelle des détails supplémentaires sur cette alerte, y compris les actions recommandées. Vous pouvez également effacer les alerte hello si hello est résolu.
* Hello **travaux** zone fournit un instantané des travaux récents sur tous les périphériques connectés tooyour service. Il existe des liens que vous pouvez utiliser toolook sur les travaux qui sont actuellement en cours, ceux qui ont échoué hello des dernières 24 heures, ou celles qui sont planifiées toorun Bonjour pendant les 24 heures.
* Hello **coup de œil rapide** zone fournit des informations utiles, telles que l’état du service, le nombre de périphériques connectés toohello service, l’emplacement du service de hello et des détails de l’abonnement hello qui est associé au service de hello. Il existe également un journal des opérations toohello lien. Cliquez sur hello lien toosee une liste de toutes les opérations de service StorSimple Manager terminée.

Vous pouvez utiliser hello StorSimple Manager service tableau de bord page tooinitiate hello tâches suivantes :

* Afficher ou régénérer la clé d’inscription hello.
* Modifier la clé de chiffrement de données de service hello.
* Afficher les journaux des opérations de hello.

## <a name="view-or-regenerate-hello-service-registration-key"></a>Afficher ou régénérer la clé d’inscription hello
clé d’inscription Hello est tooregister utilisé un appareil Microsoft Azure StorSimple avec le service StorSimple Manager hello, afin que hello périphérique s’affiche dans hello portail classique Azure pour d’autres actions de gestion. clé de Hello est créé sur le premier périphérique de hello et partagée avec rest hello de vos appareils.

En cliquant sur **clé d’inscription** (au hello en bas de page de hello) ouvre hello **clé d’inscription de Service** boîte de dialogue, dans laquelle vous pouvez soit copie hello service d’inscription toohello clé Presse-papiers actuel ou Régénérer la clé d’inscription hello.

Régénération de la clé hello n’affecte pas les périphériques déjà enregistrés : il ne concerne que les périphériques de hello qui sont inscrits avec le service de hello après hello est régénérée.

Pour plus d’informations sur l’affichage et la génération de clé, accédez de hello service d’inscription trop[clé d’inscription Get hello](storsimple-manage-service.md#get-the-service-registration-key).

## <a name="change-hello-service-data-encryption-key"></a>Modifier la clé de chiffrement de données de service hello
Clés de chiffrement de données de service sont des données client confidentielles tooencrypt utilisés, tels que les informations d’identification compte stockage qui sont envoyées à partir de votre appareil de StorSimple de toohello service StorSimple Manager. Vous devez toochange ces clés périodiquement si votre organisation a une stratégie de rotation des clés sur les périphériques de stockage hello. Hello processus de modification de la clé peut être légèrement différente selon qu’il existe un ou plusieurs périphériques gérés par hello service StorSimple Manager.

Modification hello clé de chiffrement est un processus en 3 étapes :

1. À l’aide de hello portail Azure classic, d’autoriser une périphérique toochange hello clé de chiffrement.
2. À l’aide de Windows PowerShell pour StorSimple, de lancer le changement de clé de chiffrement de hello service données.
3. Si vous avez plusieurs périphériques StorSimple, mettre à jour hello clé de chiffrement sur hello autres périphériques.

Hello étapes suivantes décrivent le processus de substitution hello pour la clé de chiffrement de données de service hello.

[!INCLUDE [storsimple-change-data-encryption-key](../../includes/storsimple-change-data-encryption-key.md)]

## <a name="view-hello-operations-logs"></a>Afficher les journaux des opérations hello
Vous pouvez afficher les journaux des opérations de hello en cliquant sur hello opération lien des journaux des Bonjour **coup de œil rapide** volet du tableau de bord hello. Cette opération prendra toohello management services, page où vous pouvez filtrer et consultez hello enregistre le service StorSimple Manager tooyour spécifique.

## <a name="next-steps"></a>Étapes suivantes
* Découvrez comment trop[dépanner un appareil StorSimple](storsimple-troubleshoot-operational-device.md).
* En savoir plus sur la façon trop[utilisez hello tooadminister du service StorSimple Manager de votre appareil StorSimple](storsimple-manager-service-administration.md).

