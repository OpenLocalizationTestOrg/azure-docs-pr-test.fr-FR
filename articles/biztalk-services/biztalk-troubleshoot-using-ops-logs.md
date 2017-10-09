---
title: "à l’aide des journaux des opérations d’aaaTroubleshoot BizTalk Services | Documents Microsoft"
description: "Résolution des problèmes BizTalk Services à l'aide des journaux des opérations. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 1081a9c6-58cc-4a76-8ac8-11e5e7a6ea27
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 102779ed6e29784f190c28e4102a7d9670614914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-troubleshoot-using-operation-logs"></a>BizTalk Services : résolution des problèmes à l’aide des journaux des opérations

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

## <a name="what-are-hello-operation-logs"></a>Que sont les journaux des opérations de hello
Journaux des opérations est une fonctionnalité de gestion des Services disponible dans hello portail classique Azure qui vous permet de tooview les journaux historiques des opérations effectuées sur vos services Azure, y compris les Services BizTalk. Cela vous permet de tooview les données d’historique des opérations de toomanagement sur votre abonnement au Service de BizTalk en remontant jusqu'à 180 jours.

> [!NOTE]
> Cette fonctionnalité capture uniquement les journaux pour les opérations de gestion sur les Services BizTalk, telles que le démarrage des services de hello, sauvegardé, et ainsi de suite. Ces opérations sont suivies indépendamment de si elles sont exécutées à partir de hello portail Azure classic ou à l’aide de hello [API REST des services BizTalk](http://msdn.microsoft.com/library/azure/dn232347.aspx). Pour obtenir la liste complète des opérations suivies à l'aide des services de gestion, consultez la rubrique [Opérations suivies à l'aide des services de gestion Azure](#bizops).<br/><br/>
> Cela ne capture pas les journaux hello pour les activités de tooBizTalk connexes runtime du Service (par exemple, les messages traités par les ponts, etc.).. tooview ces journaux, utilisez hello vue du suivi à partir du portail de Services BizTalk hello. Pour plus d'informations, consultez la rubrique [Messages de suivi](http://msdn.microsoft.com/library/azure/hh949805.aspx).
> 
> 

## <a name="view-biztalk-services-operation-logs"></a>Affichage des journaux des opérations BizTalk Services
1. Bonjour portail Azure classic, sélectionnez **des Services de gestion**, puis sélectionnez hello **journaux des opérations** onglet.
2. Vous pouvez filtrer les journaux de hello en fonction des paramètres différents, comme l’abonnement, plage de dates, le type de service (par exemple, les Services BizTalk), nom du service ou état d’opération hello (réussite, échec).
3. Sélectionnez hello coche tooview hello liste filtrée. Hello image suivante montre tootestbiztalkservice connexes des activités : ![afficher les journaux des opérations][ViewLogs] 
4. tooview en savoir plus sur une opération spécifique, sélectionnez la ligne de hello, puis cliquez sur **détails** dans la barre des tâches en bas de hello hello.

## <a name="bizops"></a>Opérations suivies à l'aide des services de gestion Azure
Hello tableau suivant répertorie les opérations hello qui sont suivies à l’aide des Services de gestion Azure hello :

| Nom d’opération | Task |
| --- | --- |
| CreateBizTalkService |Opération toocreate un BizTalk Service |
| DeleteBizTalkService |Opération toodelete un BizTalk Service |
| RestartBizTalkService |Opération toorestart un BizTalk Service |
| StartBizTalkService |Opération toostart un BizTalk Service |
| StopBizTalkService |Opération toostop un BizTalk Service |
| DisableBizTalkService |Opération toodisable un BizTalk Service |
| EnableBizTalkService |Opération tooenable un BizTalk Service |
| BackupBizTalkService |Tooback d’opération d’un BizTalk Service |
| RestoreBizTalkService |Opération toorestore un BizTalk Service à partir de la sauvegarde spécifiée |
| SuspendBizTalkService |Opération toosuspend un BizTalk Service |
| ResumeBizTalkService |Opération tooresume un BizTalk Service |
| ScaleBizTalkService |Opération tooscale un BizTalk Service vers le haut ou vers le bas |
| ConfigUpdateBizTalkService |Configuration de hello tooupdate l’opération d’un BizTalk Service |
| ServiceUpdateBizTalkService |Opération tooupgrade ou une rétrogradation d’une version différente de tooa BizTalk Service |
| PurgeBackupBizTalkService |Sauvegardes de toopurge opération Hello BizTalk Service en dehors de la période de rétention hello |

## <a name="see-also"></a>Voir aussi
* [Sauvegarde d'un service BizTalk](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [Restauration d'un service BizTalk depuis une sauvegarde](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [BizTalk Services : approvisionnement à l’aide du portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [Tableau comparatif des états d'approvisionnement BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [Onglets Tableau de bord, Surveiller et Mettre à l'échelle dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [Limitation dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [Nom et clé de l'émetteur dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [Comment puis-je démarrer à l’aide de hello SDK des Services BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[ViewLogs]: ./media/biztalk-troubleshoot-using-ops-logs/Operation-Logs.png

