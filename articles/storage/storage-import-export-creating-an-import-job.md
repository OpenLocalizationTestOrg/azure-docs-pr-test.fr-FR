---
title: "aaaCreate un travail d’importation pour Azure Import/Export | Documents Microsoft"
description: "Découvrez comment toocreate une importation de hello service Microsoft Azure Import/Export."
author: muralikk
manager: syadav
editor: syadav
services: storage
documentationcenter: 
ms.assetid: 8b886e83-6148-4149-9d0f-5d48ec822475
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: da974c33a3688bb5e2412c8bfcbeca704096c2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-import-job-for-hello-azure-importexport-service"></a>Création d’un travail d’importation pour hello service Azure Import/Export

Création d’un travail d’importation pour le service de Microsoft Azure Import/Export hello à l’aide des API REST de hello implique hello comme suit :

-   Préparation des lecteurs à hello outil d’importation/exportation Azure.

-   Obtenir le lecteur hello tooship hello emplacement toowhich.

-   Création de tâche d’importation hello.

-   Hello d’expédition des lecteurs tooMicrosoft via un service de transport pris en charge.

-   Mise à jour le travail d’importation hello avec hello détails de l’expédition.

 Consultez [à l’aide du service d’importation/exportation de Microsoft Azure hello données tooTransfer tooBlob stockage](storage-import-export-service.md) pour une vue d’ensemble du service d’importation/exportation hello et un didacticiel qui montre comment toouse hello [portail Azure](https://portal.azure.com/) toocreate et gérer l’importation et exportation des travaux.

## <a name="preparing-drives-with-hello-azure-importexport-tool"></a>Préparation des lecteurs à hello outil d’importation/exportation Azure

Hello étapes tooprepare lecteurs pour un travail d’importation sont hello même si vous créez hello portal de hello jobvia ou via hello API REST.

Voici une brève présentation de la préparation du disque. Consultez toohello [Azure Import-ExportTool référence](storage-import-export-tool-how-to-v1.md) pour des instructions complètes. Vous pouvez télécharger hello outil d’importation/exportation Azure [ici](http://go.microsoft.com/fwlink/?LinkID=301900).

La préparation de votre disque implique :

-   Identification hello toobe de données importée.

-   Identification des objets BLOB de destination hello dans le stockage Windows Azure.

-   À l’aide de toocopy d’outil d’importation/exportation Azure hello tooone de vos données ou de plusieurs disques durs.

 Hello, outil d’importation/exportation Azure génèrera également un fichier manifeste pour chacun des lecteurs de hello lors de sa préparation. Un fichier de manifeste contient les éléments suivants :

-   Énumération de tous les fichiers de hello prévus pour le téléchargement et mappages hello à partir de ces tooblobs de fichiers.

-   Sommes de contrôle des segments hello de chaque fichier.

-   Informations sur les tooassociate de métadonnées et propriétés hello avec chaque objet blob.

-   Une liste des hello action tootake si un objet blob qui est en cours de téléchargement a hello même nom qu’un objet blob existant dans le conteneur de hello. Les options possibles sont : a) remplacer l’objet blob de hello avec fichier de hello, (b) conserver l’objet blob existant de hello et ignorer le téléchargement du fichier de hello, c) ajouter un nom de toohello suffixe afin qu’il n’est pas en conflit avec d’autres fichiers.

## <a name="obtaining-your-shipping-location"></a>Obtention de votre emplacement d’expédition

Avant de créer un travail d’importation, vous avez besoin tooobtain un nom d’emplacement d’expédition et l’adresse en appelant hello [liste des emplacements](/rest/api/storageimportexport/listlocations) opération. `List Locations` renvoie une liste d’emplacements et leurs adresses postales. Vous pouvez sélectionner un emplacement à partir de hello retourné liste et votre adresse de toothat de disques durs de livraison. Vous pouvez également utiliser hello `Get Location` hello de tooobtain opération copie les adresses pour un emplacement spécifique directement.

 Suivez les étapes de hello sous l’emplacement d’expédition tooobtain hello :

-   Identifier le nom hello d’emplacement hello de votre compte de stockage. Cette valeur peut être trouvée sous hello **emplacement** champ du compte de stockage hello **tableau de bord** Bonjour portail Azure ou interrogé à l’aide d’opération de l’API de gestion des services hello [obtenir le stockage Propriétés de compte](/rest/api/storagerp/storageaccounts#StorageAccounts_GetProperties).

-   Récupérer emplacement hello tooprocess disponibles à ce compte de stockage en appelant hello `Get Location` opération.

-   Si hello `AlternateLocations` propriété d’emplacement de hello contient l’emplacement hello lui-même, puis il est OK toouse cet emplacement. Sinon, appelez hello `Get Location` opération en utilisant un des emplacements de remplacement hello. emplacement d’origine de Hello peut être fermé temporairement pour maintenance.

## <a name="creating-hello-import-job"></a>Création du travail d’importation hello
travail d’importation toocreate hello, appel hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) opération. Vous devez hello tooprovide informations suivantes :

-   Un nom pour la tâche de hello.

-   nom de compte de stockage Hello.

-   Hello obtenu à l’étape précédente de hello nom de l’emplacement d’expédition.

-   Type de travail (importation).

-   adresse de retour Hello laquelle hello lecteurs doivent être envoyés une fois le travail d’importation hello est terminée.

-   liste Hello de lecteurs dans la tâche de hello. Pour chaque lecteur, vous devez inclure hello informations a été obtenues pendant l’étape de préparation du lecteur hello suivantes :

    -   Id de lecteur Hello

    -   clé de BitLocker Hello

    -   chemin d’accès relatif Hello fichier manifeste sur le disque dur hello

    -   Hello Base16 encodé hachage MD5 de fichier manifeste

## <a name="shipping-your-drives"></a>Expédition de vos disques
Vous devez expédier votre adresse de toohello de disques que vous avez obtenue à partir de l’étape précédente de hello, et vous devez fournir hello service Import/Export avec hello suivi du numéro de package de hello.

> [!NOTE]
>  Vous devez expédier vos disques via un service de transport pris en charge, qui vous fournira un numéro de suivi pour votre colis.

## <a name="updating-hello-import-job-with-your-shipping-information"></a>Mise à jour de la tâche d’importation hello avec vos informations d’expédition
Après avoir configuré votre numéro de suivi, appelez hello [Update Job Properties](/api/storageimportexport/jobs#Jobs_Update) hello de tooupdate opération copie le nom de l’opérateur, le numéro de suivi hello du travail de hello et hello compte du transporteur pour les retours. Vous pouvez éventuellement spécifier le nombre de hello des lecteurs et hello date d’expédition.

## <a name="next-steps"></a>Étapes suivantes

* [À l’aide des API REST du service importation/exportation hello](storage-import-export-using-the-rest-api.md)
