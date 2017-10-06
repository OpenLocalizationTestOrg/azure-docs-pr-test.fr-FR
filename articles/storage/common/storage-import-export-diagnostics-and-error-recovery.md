---
title: "aaaDiagnostics et la récupération pour les travaux d’importation/exportation Azure | Documents Microsoft"
description: "Découvrez comment les tâches de service de la journalisation documentée tooenable pour Microsoft Azure Import/Export."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 48164279e7904c78fed802aa3cff66e589c3f12c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a>Diagnostic et récupération d’erreur pour les travaux Azure Import/Export
Pour chaque lecteur traité, hello service Azure Import/Export crée un journal des erreurs dans le compte de stockage hello associé. Vous pouvez également activer la journalisation détaillée en définissant un hello `LogLevel` propriété trop`Verbose` lors de l’appel hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.

 Par défaut, les journaux sont écrits conteneur tooa nommé `waimportexport`. Vous pouvez spécifier un nom différent en définissant la hello `DiagnosticsPath` propriété lors de l’appel hello `Put Job` ou `Update Job Properties` operations. Hello journaux sont stockés en tant qu’objets BLOB de blocs avec hello respectent les conventions d’affectation de noms : `waies/jobname_driveid_timestamp_logtype.xml`.

 Vous pouvez récupérer hello URI des journaux hello pour un travail en appelant hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) opération. Hello URI pour la journalisation documentée hello est retourné dans hello `VerboseLogUri` propriété pour chaque lecteur, alors que hello URI hello journal des erreurs est retourné dans hello `ErrorLogUri` propriété.

Vous pouvez utiliser hello journalisation hello tooidentify de données suivants.

## <a name="drive-errors"></a>Erreurs de disque

Hello éléments suivants est classé en tant qu’erreurs de lecteur :

-   Erreurs dans l’accès ou hello lors de la lecture du fichier manifeste

-   Clés BitLocker incorrectes

-   Erreurs de lecture/écriture sur le disque

## <a name="blob-errors"></a>Erreurs d’objet blob

Hello éléments suivants est classée comme des erreurs de l’objet blob :

-   Objet blob ou nom incorrect ou conflictuel

-   Fichiers manquants

-   Objet blob introuvable

-   Fichiers tronqués (fichiers hello sur le disque de hello sont plus petits que ceux spécifiés dans le manifeste de hello)

-   Contenu de fichier endommagé (pour les travaux d’importation, détecté par une incompatibilité de la somme de contrôle MD5)

-   Fichiers de propriétés et de métadonnées blob endommagés (détectés par une incompatibilité de la somme de contrôle MD5)

-   Schéma incorrect pour les propriétés d’objet blob hello et/ou les fichiers de métadonnées

Il peut arriver dans laquelle certaines parties d’un travail d’importation ou d’exportation n’aboutissent pas, alors que hello globale travail est terminé. Dans ce cas, vous pouvez soit charger ou télécharger hello manquant hello données sur le réseau, ou vous pouvez créer les données de salutation un nouveau travail tootransfer. Consultez hello [référence de l’outil Azure Import/Export](storage-import-export-tool-how-to-v1.md) toolearn comment toorepair hello des données sur le réseau.

## <a name="next-steps"></a>Étapes suivantes

* [À l’aide des API REST du service importation/exportation hello](storage-import-export-using-the-rest-api.md)
