---
title: aaaCancel et supprimer un travail Azure Import/Export | Documents Microsoft
description: "Découvrez comment toocancel et supprimer des travaux pour hello service Microsoft Azure Import/Export."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 5d2aba510dafd0ca9a10f5643f721e7059a6a8f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a>Annulation et suppression de travaux du service Azure Import/Export

Vous pouvez demander qu’une tâche annulée avant qu’il soit Bonjour `Packaging` état en appelant hello [propriétés de tâche de mise à jour](/rest/api/storageimportexport/jobs#Jobs_Update) opération et le paramètre hello `CancelRequested` élément trop`true`. tâche de Hello sera annulée de manière optimale. Si les lecteurs sont en cours de hello de transfert de données, les données peuvent continuer toobe transférée même après que l’annulation a été demandée.

 Un travail annulé déplacera toohello `Completed` d’état et conservé pendant 90 jours, à quel point il sera supprimé.

 toodelete un travail, appel hello [supprimer le travail](/rest/api/storageimportexport/jobs#Jobs_Delete) opération avant que le travail de hello a été expédiée (*c'est-à-dire*, tandis que le travail de hello est Bonjour `Creating` état). Vous pouvez également supprimer un travail lorsqu’il est Bonjour `Completed` état. Après la suppression d’un travail, ses informations et l’état ne sont plus accessibles via l’API REST de hello ou hello portail Azure.

## <a name="next-steps"></a>Étapes suivantes

* [À l’aide des API REST du service importation/exportation hello](storage-import-export-using-the-rest-api.md)
