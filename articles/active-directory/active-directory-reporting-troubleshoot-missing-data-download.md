---
title: "Résolution des problèmes : Les données manquantes dans hello téléchargement les journaux d’activité Azure Active Directory | Documents Microsoft"
description: "Vous fournit des données toomissing résolution dans le journal d’activité de Azure Active Directory téléchargé."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a>Impossible de trouver des données dans les journaux d’activité Azure Active Directory hello téléchargés


## <a name="symptoms"></a>Symptômes

Télécharger les journaux d’activité hello (audit ou connexions) et ne sont pas tous les enregistrements de hello pendant hello, que vous avez choisi. Pourquoi ? 

 ![Reporting](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a>Cause :

Lorsque vous téléchargez les journaux d’activité Bonjour portail Azure, nous limitons enregistrements too120K hello échelle triés par la plupart des récentes. 

## <a name="resolution"></a>Résolution :

Vous pouvez tirer parti de [API de création de rapports AD Azure](active-directory-reporting-api-getting-started.md) toofetch des enregistrements tooa millions à un moment donné. Notre approche recommandée est toorun un script selon une planification qui appelle hello reporting API toofetch enregistre de manière incrémentielle sur une période de temps (par exemple, quotidienne ou hebdomadaire).

## <a name="next-steps"></a>Étapes suivantes
Consultez hello [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).

