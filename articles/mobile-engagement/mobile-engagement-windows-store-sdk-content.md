---
title: aaaWindows contenu applications universelles
description: "En savoir plus sur contenu hello Hello SDK d’applications universelles Windows pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a8013d2433c0be62d737c8bc6e8360ed79bbe532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-content"></a>Contenu du Kit de développement logiciel (SDK) des applications Windows Universal
Ce document répertorie et décrit le contenu de hello déployé par hello SDK dans votre application.

## <a name="hello-resources-folder"></a>Hello `/Resources` dossier
Ce dossier contient toutes les ressources de hello Mobile Engagement a besoin. Vous pouvez également personnaliser toofit votre application.

* `EngagementConfiguration.xml`: hello du fichier de configuration Mobile Engagement, il s’agit d’où vous pouvez personnaliser les paramètres de Mobile Engagement (chaîne de connexion de Mobile Engagement, panne de rapport...).

### <a name="html-folder"></a>Dossier /html
* `EngagementNotification.html`: hello `Notification` conception html d’affichage pour les bannières dans l’application web.
* `EngagementAnnouncement.html`: hello `Announcement` conception html d’affichage pour les vues spots dans l’application web.

### <a name="images-folder"></a>Dossier /images
* `EngagementIconNotification.png`: hello marque icône à hello à gauche d’une notification, remplacez celui-ci par une icône de la marque.
* `EngagementIconOk.png`: hello `Ok` icône hello portée de pages de contenu pour le bouton d’action ou validation hello.
* `EngagementIconNOK.png`: hello `NOK` icône utilisée lorsque le bouton de validation hello hello portée de pages de contenu est désactivé.
* `EngagementIconClose.png`: hello `Close` icône Hello atteindre des notifications et de contenu pour hello fermer bouton.

### <a name="overlay-folder"></a>Dossier /overlay
* `EngagementPageOverlay.cs`: page de segment de recouvrement hello responsables de l’ajout de hello Engagement atteindre l’enfant de tooits de l’interface utilisateur dans l’application.

