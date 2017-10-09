---
title: "informations sur l’état d’un travail d’importation/exportation Azure aaaRetrieving | Documents Microsoft"
description: "Découvrez comment tooobtain informations d’état de travaux du service Microsoft Azure Import/Export."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 22d7e5f0-94da-49b4-a1ac-dd4c14a423c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: muralikk
ms.openlocfilehash: cbc35660519573d92f641924ac0025c9e577d69b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="retrieving-state-information-for-an-importexport-job"></a>Récupération des informations d’état d’un travail Import/Export
Vous pouvez appeler hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) opération tooretrieve informations deux importer et exporter des travaux. Hello les informations retournées incluent :

-   état actuel de Hello du travail de hello.

-   pourcentage approximatif de Hello que chaque tâche est terminée.

-   état actuel de Hello de chaque lecteur.

-   Les URI des blobs contenant les journaux d’erreurs et des informations de journalisation détaillées (si activé).

Hello sections suivantes expliquent les informations de hello retournées par hello `Get Job` opération.

## <a name="job-states"></a>États de travail
table de Hello et diagramme d’état hello ci-dessous décrivent les États hello un travail passe par pendant son cycle de vie. état actuel de Hello du travail de hello peut être déterminé en appelant hello `Get Job` opération.

![JobStates](./media/storage-import-export-retrieving-state-info-for-a-job/JobStates.png "JobStates")

Hello tableau suivant décrit chaque état dans lequel une tâche peut passer.

|État du travail|Description|
|---------------|-----------------|
|`Creating`|Une fois que vous appelez l’opération Put Job de hello, une tâche est créée et son état est défini trop`Creating`. Pendant que le travail de hello est Bonjour `Creating` d’état, hello service d’importation/exportation suppose hello lecteurs n’ont pas été expédiés toohello Datacenter. Un travail peut rester dans hello `Creating` état pour les semaines tootwo, après laquelle il est automatiquement supprimé par le service de hello.<br /><br /> Si vous appelez opération Update Job Properties de hello pendant hello tâche Bonjour `Creating` l’état, la tâche de hello reste Bonjour `Creating` d’état et hello de délai d’attente intervalle est réinitialisation tootwo semaines.|
|`Shipping`|Après avoir expédié votre package, vous devez appeler hello Update Job Properties opération mise à jour hello d’état du travail de hello trop`Shipping`. Hello état d’expédition peut être définie uniquement si hello `DeliveryPackage` (transporteur et numéro de suivi) et hello `ReturnAddress` propriétés ont été définies pour le travail de hello.<br /><br /> travail de Hello reste en état d’expédition hello pour les tootwo semaines. Si les deux semaines ont réussi et hello lecteurs n’ont pas été reçus, opérateurs de service d’importation/exportation hello soient prévenus.|
|`Received`|Une fois que tous les lecteurs ont été reçues au centre de données hello, état de la tâche hello définira toohello état Received.|
|`Transferring`|Une fois hello lecteurs ont été reçus au centre de données hello et au moins un lecteur a commencé le traitement, état de la tâche hello définira toohello `Transferring` état. Consultez hello `Drive States` section ci-dessous pour plus d’informations.|
|`Packaging`|Une fois que tous les lecteurs ont terminé le traitement, hello travail est placé dans hello `Packaging` état jusqu'à ce que les lecteurs hello sont expédiés toohello précédent client.|
|`Completed`|Une fois que tous les lecteurs ont été expédiés toohello précédent client, si hello est terminée sans erreur, puis les travaux hello seront défini toohello `Completed` état. Hello travail sera automatiquement supprimé après 90 jours Bonjour `Completed` état.|
|`Closed`|Une fois que tous les lecteurs ont été expédiés toohello précédent client, si des erreurs ont été lors du traitement de hello du travail de hello, puis les travaux hello seront défini toohello `Closed` état. Hello travail sera automatiquement supprimé après 90 jours Bonjour `Closed` état.|

Vous pouvez annuler un travail uniquement lorsqu’il est défini sur certains états. Un travail annulé ignore l’étape de copie des données hello, mais sinon il suit hello même transitions d’état en tant que tâche qui n’a pas été annulée.

Hello tableau suivant décrit les erreurs qui peuvent se produire pour chaque état de la tâche, ainsi que sur l’effet hello sur le travail de hello lorsqu’une erreur se produit.

|État du travail|Événement|Résolution/Étapes suivantes|
|---------------|-----------|------------------------------|
|`Creating or Undefined`|Un ou plusieurs disques pour un travail est arrivé, mais les travaux hello ne sont pas hello `Shipping` état ou il n’existe aucun enregistrement de la tâche hello dans le service hello.|équipe des opérations de service importation/exportation Hello sera essayez toocontact hello client toocreate ou mettre à jour de la tâche de hello avec la tâche avant des informations nécessaires toomove hello.<br /><br /> Si l’équipe des opérations hello est client de hello toocontact impossible dans les deux semaines, équipe hello tentera tooreturn hello lecteurs.<br /><br /> Dans l’événement hello hello lecteurs ne peuvent pas être retournés et client de hello n’est pas accessible, hello lecteurs seront détruits en toute sécurité dans les 90 jours.<br /><br /> Notez qu’une tâche ne peut pas être traitée tant que son état est mis à jour trop`Shipping`.|
|`Shipping`|package Hello pour un travail n’est pas arrivé pour plus de deux semaines.|équipe Hello informera client hello de package manquant de hello. En fonction de la réponse du client hello, équipe hello sera étendez toowait d’intervalle hello pour hello package tooarrive, ou annuler la tâche de hello.<br /><br /> En cas de hello client hello ne peut pas être contacté ou ne répond pas dans les 30 jours, équipe hello va lancer le travail de hello toomove action à partir de hello `Shipping` état directement toohello `Closed` état.|
|`Completed/Closed`|lecteurs Hello jamais atteint l’adresse de retour hello ou ont été endommagés lors de l’expédition (s’applique le travail d’exportation tooan uniquement).|Si les lecteurs hello n’atteignent pas l’adresse de retour hello, client de hello doit première appeler une opération Get Job hello ou vérification du statut de tâche hello dans hello tooensure portail que hello lecteurs ont été expédiés. Si les lecteurs hello ont été expédiés, client de hello doit contacter hello expédition fournisseur tootry et localiser les lecteurs hello.<br /><br /> Hello lecteurs sont endommagés pendant l’expédition, les clients hello préférable toorequest un autre travail d’exportation ou d’objets BLOB manquants de téléchargement hello.|
|`Transferring/Packaging`|L’adresse de retour est incorrecte ou manquante.|équipe Hello va joindre toohello personne à contacter pour l’adresse correcte hello travail tooobtain hello.<br /><br /> En cas de hello client hello n’est pas accessible, hello lecteurs seront détruits de manière sécurisée dans les 90 jours.|
|`Creating / Shipping/ Transferring`|Un lecteur qui n’apparaît pas dans la liste hello de toobe lecteurs importé est inclus dans hello copie le package.|Hello lecteurs supplémentaires ne seront pas traités et seront affichera toohello client lorsque hello tâche est terminée.|

## <a name="drive-states"></a>États du disque
table de Hello et diagramme hello ci-dessous décrivent le cycle de vie de hello d’un lecteur individuel lorsqu’il passe par un travail d’importation ou d’exportation. Vous pouvez récupérer l’état du lecteur actif hello en appelant hello `Get Job` opération et en inspectant hello `State` élément Hello `DriveList` propriété.

![DriveStates](./media/storage-import-export-retrieving-state-info-for-a-job/DriveStates.png "DriveStates")

Hello tableau suivant décrit chaque état dans lequel un lecteur peut passer.

|État du disque|Description|
|-----------------|-----------------|
|`Specified`|Pour un travail d’importation, lorsque le travail de hello est créé par hello opération Put Job, état initial de hello pour un lecteur est hello `Specified` état. Pour un travail d’exportation, car aucun lecteur n’est spécifié lors de la tâche de hello est créée, état initial du lecteur de hello est hello `Received` état.|
|`Received`|lecteur de Hello entre toohello `Received` d’état lorsque hello opérateur du service d’importation/exportation a traité les lecteurs hello qui ont été reçus à partir de hello entreprise pour un travail d’importation de livraison. Pour un travail d’exportation, état initial du lecteur de hello est hello `Received` état.|
|`NeverReceived`|lecteur de Hello entre toohello `NeverReceived` état lorsque hello le package pour un travail arrive mais hello ne contient pas le lecteur de hello. Un lecteur peut également déplacer dans cet état si elle a été deux semaines, car le service de hello reçu les informations d’expédition hello, mais le package de hello n’a pas encore arrivé au centre de données hello.|
|`Transferring`|Un lecteur entre toohello `Transferring` d’état lorsque hello service commence tootransfer les données à partir de hello lecteur tooWindows le stockage Azure.|
|`Completed`|Un lecteur entre toohello `Completed` lorsque hello service a correctement transféré toutes les données hello sans erreurs d’état.|
|`CompletedMoreInfo`|Un lecteur entre toohello `CompletedMoreInfo` toohello ou lorsque hello service a rencontré des problèmes lors de la copie des données à partir de l’état. informations de Hello peuvent inclure des erreurs, des avertissements ou messages d’information concernant le remplacement des objets BLOB.|
|`ShippedBack`|lecteur de Hello entre toohello `ShippedBack` état lorsqu’il a été livré à partir de l’adresse de retour hello données centre toohello.|

Hello tableau suivant décrit États d’échec lecteur hello et les actions de hello effectuées pour chaque état.

|État du disque|Événement|Résolution / Étape suivante|
|-----------------|-----------|-----------------------------|
|`NeverReceived`|Un lecteur qui est marqué comme étant `NeverReceived` (car il n’a pas été reçu dans le cadre de l’expédition du travail hello) arrive dans une autre expédition.|équipe Hello déplacera hello lecteur toohello `Received` état.|
|`N/A`|Un lecteur qui ne fait pas partie d’un travail arrive au centre de données hello dans le cadre d’une autre tâche.|lecteur de Hello sera marquée comme un lecteur supplémentaire et est renvoyée toohello client lors de la tâche hello associé au package d’origine de hello est terminée.|

## <a name="faulted-states"></a>États d’échec
Lorsqu’une tâche ou un lecteur échoue tooprogress normalement par le biais de son cycle de vie prévue, hello travail ou un lecteur est déplacé vers un `Faulted` état. À ce stade, équipe hello contacte client hello par courrier électronique ou par téléphone. Une fois hello problème résolu, hello a généré une erreur de la tâche ou le lecteur extraite de hello `Faulted` état et déplacées dans hello appropriée état.

## <a name="next-steps"></a>Étapes suivantes

* [À l’aide des API REST du service importation/exportation hello](storage-import-export-using-the-rest-api.md)
