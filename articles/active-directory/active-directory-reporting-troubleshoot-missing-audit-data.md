---
title: "Résolution des problèmes : Données manquantes dans le journal d’activité Azure Active Directory | Microsoft Docs"
description: "Répertorie les différents rapports disponibles pour Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 47617f8f727027de113a0f503308c8accc58859e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-some-actions-that-i-performed-in-the-azure-active-directory-activity-log"></a>Je ne trouve pas certaines actions que j’ai réalisées dans le journal d’activité d’Azure Active Directory


## <a name="symptoms"></a>Symptômes

J’ai réalisé certaines actions dans le portail Azure et je pensais pouvoir consulter les journaux d’audit associés dans le panneau `Activity logs > Audit Logs`, mais je ne les trouve pas.

 ![Reporting](./media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a>Cause :

Les actions n’apparaissent pas immédiatement dans le journal d’audit des activités. Entre 15 minutes et 1 heure peuvent être nécessaires pour que les journaux d’audit s’affichent dans le portail après l’exécution de l’opération.

## <a name="resolution"></a>Résolution :

Attendez entre 15 minutes et 1 heure pour voir si les actions apparaissent dans le journal. Si elles n’apparaissent toujours pas, veuillez créer un ticket de support pour que nous résolvions le problème.


## <a name="next-steps"></a>Étapes suivantes
Consultez le [FAQ sur les rapports Azure Active Directory](active-directory-reporting-faq.md).

