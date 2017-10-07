---
title: "aaaHow toosend planifiée notifications | Documents Microsoft"
description: "Cette rubrique décrit l'utilisation de notifications planifiées avec Azure Notification Hubs."
services: notification-hubs
documentationcenter: .net
keywords: notifications push,notification push,planification de notifications push
author: ysxu
manager: erikre
editor: 
ms.assetid: 6b718c75-75dd-4c99-aee3-db1288235c1a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 9b3ba715dad6f5d824a615e83f2863b0db47b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-send-scheduled-notifications"></a>Procédure : envoi de notifications planifiées
## <a name="overview"></a>Vue d'ensemble
Si vous avez un scénario dans lequel toosend une notification à un moment donné dans hello futures, mais vous n’avez pas une toowake facilement votre notification de hello toosend code principal. Concentrateurs de Notification de niveau standard prend en charge une fonctionnalité qui vous permet de notifications tooschedule jours too7 Bonjour futures.

Lorsque vous envoyez une notification, utilisez simplement hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) classe Bonjour SDK de concentrateurs de Notification, comme indiqué dans hello l’exemple suivant :

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

Vous pouvez également annuler une notification précédemment planifiée à l'aide de son ID de notification :

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

Il n’existe aucune limite sur le nombre de hello de notifications planifiées que vous pouvez envoyer.

