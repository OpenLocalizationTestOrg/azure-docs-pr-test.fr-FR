---
title: "aaaCreate une exportation de la tâche d’importation/exportation Azure | Documents Microsoft"
description: "Découvrez comment toocreate une exportation de la tâche pour hello service Microsoft Azure Import/Export."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 613d480b-a8ef-4b28-8f54-54174d59b3f4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 4a10b42cc86dbf3bcea3a515bc065e2259228ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-export-job-for-hello-azure-importexport-service"></a>Création d’un travail d’exportation pour hello service Azure Import/Export
Création d’un travail d’exportation pour le service de Microsoft Azure Import/Export hello à l’aide des API REST de hello implique hello comme suit :

-   En sélectionnant hello tooexport des objets BLOB.

-   Obtention d’un emplacement d’expédition.

-   Création de travail d’exportation hello.

-   Expédition tooMicrosoft de vos lecteurs vides via un service de transport pris en charge.

-   Mise à jour le travail d’exportation hello avec les informations de package hello.

-   Lecteurs hello réception expédiés par Microsoft.

 Consultez [à l’aide du service d’importation/exportation de Windows Azure hello données tooTransfer tooBlob stockage](storage-import-export-service.md) pour une vue d’ensemble du service d’importation/exportation hello et un didacticiel qui montre comment toouse hello [portail Azure](https://portal.azure.com/) toocreate et gérer l’importation et exportation des travaux.

## <a name="selecting-blobs-tooexport"></a>Sélection d’objets BLOB tooexport
 toocreate un travail d’exportation, vous devez tooprovide une liste d’objets BLOB que vous souhaitez tooexport à partir de votre compte de stockage. Il existe plusieurs façons tooselect BLOB toobe exporté :

-   Vous pouvez utiliser un tooselect de chemin d’accès relatif blob un seul objet blob et tous ses instantanés.

-   Vous pouvez utiliser un tooselect de chemin d’accès relatif blob un seul objet blob à l’exclusion de ses instantanés.

-   Vous pouvez utiliser un chemin d’accès de l’objet blob relatif et un tooselect de temps un seul instantané de capture instantanée.

-   Vous pouvez utiliser un tooselect de préfixe d’objet blob tous les objets BLOB et instantanés avec hello préfixe.

-   Vous pouvez exporter tous les objets BLOB et captures instantanées dans le compte de stockage hello.

 Pour plus d’informations sur la spécification d’objets BLOB tooexport, consultez hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) opération.

## <a name="obtaining-your-shipping-location"></a>Obtention de votre emplacement d’expédition
Avant de créer un travail d’exportation, vous avez besoin tooobtain un nom d’emplacement d’expédition et l’adresse en appelant hello [obtenir l’emplacement](https://portal.azure.com) ou [liste des emplacements](/rest/api/storageimportexport/listlocations) opération. `List Locations` renvoie une liste d’emplacements et leurs adresses postales. Vous pouvez sélectionner un emplacement à partir de hello retourné liste et votre adresse de toothat de disques durs de livraison. Vous pouvez également utiliser hello `Get Location` hello de tooobtain opération copie les adresses pour un emplacement spécifique directement.

Suivez les étapes de hello sous l’emplacement d’expédition tooobtain hello :

-   Identifier le nom hello d’emplacement hello de votre compte de stockage. Cette valeur peut être trouvée sous hello **emplacement** champ du compte de stockage hello **tableau de bord** dans classic hello portail ou interrogé à l’aide d’opération de l’API de gestion des services hello [obtenir Propriétés de compte de stockage](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Récupérer emplacement hello qui sont disponibles tooprocess ce compte de stockage en appelant hello `Get Location` opération.

-   Si hello `AlternateLocations` propriété d’emplacement de hello contient l’emplacement hello lui-même, puis il est OK toouse cet emplacement. Sinon, appelez hello `Get Location` opération en utilisant un des emplacements de remplacement hello. emplacement d’origine de Hello peut être fermé temporairement pour maintenance.

## <a name="creating-hello-export-job"></a>Création du travail d’exportation hello
 travail d’exportation toocreate hello, appel hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) opération. Vous devez hello tooprovide informations suivantes :

-   Un nom pour la tâche de hello.

-   nom de compte de stockage Hello.

-   Hello copie le nom de l’emplacement, obtenu à l’étape précédente de hello.

-   Type de travail (exportation).

-   adresse de retour Hello laquelle hello lecteurs doivent être envoyés une fois le travail d’exportation hello est terminée.

-   Bonjour toobe liste d’objets BLOB (ou préfixes d’objet blob) exporté.

## <a name="shipping-your-drives"></a>Expédition de vos disques
 Ensuite, utilisez hello outil d’importation/exportation Azure toodetermine hello nombre de lecteurs que vous devez toosend, en fonction de BLOB hello que vous avez sélectionné toobe exporté et hello taille du lecteur. Consultez hello [référence de l’outil Azure Import/Export](storage-import-export-tool-how-to-v1.md) pour plus d’informations.

 Lecteurs hello de package dans un même package et expédiez-les toohello adresse obtenue Bonjour étape antérieure. Notez hello suivi du numéro de votre package pour l’étape suivante de hello.

> [!NOTE]
>  Vous devez expédier vos disques via un service de transport pris en charge, qui vous fournira un numéro de suivi pour votre colis.

## <a name="updating-hello-export-job-with-your-package-information"></a>Mise à jour de la tâche d’exportation hello avec les informations de package
 Après avoir configuré votre numéro de suivi, appelez hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) nom d’opération tooupdated hello transporteur et numéro hello travail de suivi. Vous pouvez éventuellement spécifier le nombre de hello de lecteurs, l’adresse de retour hello et hello date d’expédition.

## <a name="receiving-hello-package"></a>Réception hello package
 Une fois votre travail d’exportation a été traité, vos lecteurs seront affichera tooyou avec vos données chiffrées. Vous pouvez récupérer la clé de BitLocker hello pour chacun des lecteurs hello en appelant hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) opération. Vous pouvez déverrouiller lecteur hello à l’aide de la clé de hello. fichier manifeste de lecteur Hello sur chaque lecteur contient hello liste des fichiers sur le lecteur de hello, ainsi que d’adresse d’objet blob d’origine hello pour chaque fichier.

## <a name="next-steps"></a>Étapes suivantes

* [À l’aide des API REST du service importation/exportation hello](storage-import-export-using-the-rest-api.md)
