---
title: "aaaAzure présentation du kit SDK de Mobile Engagement Windows Phone Silverlight | Documents Microsoft"
description: "Vue d’ensemble de hello Windows Phone Silverlight SDK pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 0e3d2420-0509-4952-8891-392e3dad9aaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 11/03/2016
ms.author: piyushjo
ms.openlocfilehash: ff2febed2202127e0538373ebbabe674993ce39d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-sdk-overview-for-azure-mobile-engagement"></a>Vue d'ensemble du Kit de développement Silverlight de Windows Phone pour Azure Engagement Mobile
Démarrer les détails de hello tooget ici sur la façon de toointegrate Azure Mobile Engagement dans une application Silverlight de Windows Phone. Si vous souhaitez que toogive il essayer en premier lieu, assurez-vous que vous exécuter notre [didacticiel de 15 minutes](mobile-engagement-windows-phone-get-started.md).

Cliquez sur toosee hello [contenu du Kit de développement logiciel](mobile-engagement-windows-phone-sdk-content.md)

## <a name="integration-procedures"></a>Procédures d'intégration
1. Démarrez ici : [comment toointegrate Mobile Engagement dans votre application Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
2. Pour les Notifications : [comment toointegrate portée (Notifications) dans votre application Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement-reach.md)
3. Implémentation d’un plan de la balise : [comment toouse hello avancé Mobile Engagement marquage API dans votre application Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md)

## <a name="release-notes"></a>Notes de publication
###<a name="331-11032016"></a>3.3.1 (11/03/2016)
Partie de hello *MicrosoftAzure.MobileEngagement* package Nuget **v3.4.1**

* Améliorations de la stabilité.

Pour les versions antérieures, consultez hello [terminer les notes de publication](mobile-engagement-windows-phone-release-notes.md)

## <a name="upgrade-procedures"></a>Procédures de mise à niveau
Si vous avez déjà intégré une ancienne version de notre kit de développement logiciel dans votre application, vous avez hello tooconsider hello Kit de développement logiciel de la mise à niveau les points suivants.

Vous avez peut-être toofollow plusieurs procédures issue de plusieurs versions du Kit de développement logiciel de hello. Consultez hello complète [mise à niveau des procédures](mobile-engagement-windows-phone-upgrade-procedure.md). Par exemple, si vous migrez à partir de 0.10.1 too0.11.0 avoir toofirst suivez hello » à partir de 0.9.0 too0.10.1 « procédure puis hello » à partir de 0.10.1 too0.11.0 « procédure.

### <a name="from-200-too330"></a>À partir de 2.0.0 too3.3.0
#### <a name="test-logs"></a>Journaux des tests
Journaux de la console produits par hello SDK peuvent être activé/désactivé/filtrées. toocustomize, propriété hello de mise à jour `EngagementAgent.Instance.TestLogEnabled` tooone de valeur hello disponible à partir de hello `EngagementTestLogLevel` énumération, par exemple :

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="upgrade-from-older-versions"></a>Mise à niveau à partir de versions antérieures
Consultez la rubrique [Procédures de mise à niveau](mobile-engagement-windows-phone-upgrade-procedure.md)

