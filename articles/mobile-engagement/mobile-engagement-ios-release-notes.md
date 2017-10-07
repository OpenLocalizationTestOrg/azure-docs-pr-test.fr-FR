---
title: aaaAzure Mobile Engagement iOS Notes de publication SDK | Documents Microsoft
description: "Dernières mises à jour et procédures du Kit de développement logiciel (SDK) iOS pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a>Notes de publication du Kit de développement logiciel (SDK) Azure Mobile Engagement pour iOS

## <a name="410-07172017"></a>4.1.0 (07/17/2017)
* Correction des badges effacés en arrière-plan.
* Correction des avertissements sur XCode 9 à propos des API qui ne sont pas appelées dans la file d’attente principale.
* Correction d’une fuite de mémoire dans les sondages Reach.
* Fin de la prise en charge d’iOS 6.X. À partir de cette cible de déploiement hello version de votre application doit être au moins iOS 7.

## <a name="401-12132016"></a>4.0.1 (13/12/2016)
* Amélioration de la remise de journaux en arrière-plan.

## <a name="400-09122016"></a>4.0.0 (09/12/2016)
* Résolution de la notification non affichée sur les appareils iOS 10.
* Utilisation de XCode 7 déconseillée.

## <a name="324-06302016"></a>3.2.4 (30/06/2016)
* Agrégation fixe entre les journaux techniques et les autres journaux.

## <a name="323-06072016"></a>3.2.3 (07/06/2016)
* Bogue hello fixe dans lequel les commentaires de remise ne sont pas signalée lors de l’application est dans l’arrière-plan de hello.
* Hello optimisé envoi de journaux techniques.

## <a name="322-04072016"></a>3.2.2 (04/07/2016)
* Bogue d’annulation de demande HTTP conduisant parfois toocrash.

## <a name="321-12112015"></a>3.2.1 (12/11/2015)
* Délai fixe hello lorsqu’une nouvelle instance de l’application est déclenchée par une notification avec des liens profonds

## <a name="320-10082015"></a>3.2.0 (10/08/2015)
* Activé Bitcode dans toomake du Kit de développement logiciel hello elle fonctionne avec **Xcode 7**.
* Bogues résolus relatives des notifications de l’application de tooin.
* Rendu les notifications dans l’application hello plus fiable en cas de batterie faible et d’autres cas de figure.
* Suppression des journaux de console supplémentaires générés par la bibliothèque tierce.

## <a name="310-08262015"></a>3.1.0 (26/08/2015)
* Résolution d’un bogue de compatibilité iOS 9 avec une bibliothèque tierce. Ce bogue provoquait des blocages pendant l’envoi des résultats des sondages, d’informations sur l’application ou de données supplémentaires.

## <a name="300-06192015"></a>3.0.0 (19/06/2015)
* Mobile Engagement utilise des notifications Push Silent.
* Prise en charge d’iOS 4.X abandonnée. À partir de cette cible de déploiement hello version de votre application doit être au moins iOS 6.

## <a name="220-05212015"></a>2.2.0 (21/05/2015)
* id de périphérique Mobile Engagement Hello pour les appareils < iOS 6 est désormais basée sur un GUID généré au moment de l’installation.

## <a name="210-04242015"></a>2.1.0 (24/04/2015)
* Compatibilité Swift ajoutée.
* Lorsque vous cliquez sur une notification, action hello QU'URL est désormais exécutée droite après que l’application hello est ouvert.
* Ajout du fichier d'en-tête manquant dans le package du Kit de développement logiciel (SDK).
* Correction d’un problème lors de la reporter d’incident hello Mobile Engagement a été désactivée.

## <a name="200-02172015"></a>2.0.0 (17/02/2015)
* Version initiale d'Azure Engagement Mobile
* La configuration d'appId/sdkKey est remplacée par une configuration de chaîne de connexion.
* Supprimé API toosend et recevoir des messages XMPP arbitraires à partir des entités XMPP arbitraires.
* Supprimé toosend d’API et de recevoir des messages entre les appareils.
* Améliorations de sécurité.
* Suppression du suivi SmartAd.
