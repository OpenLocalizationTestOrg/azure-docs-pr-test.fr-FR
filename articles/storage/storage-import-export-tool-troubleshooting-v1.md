---
title: "aaaTroubleshooting hello outil d’importation/exportation Azure | Documents Microsoft"
description: "En savoir plus sur les problèmes courants de hello visibles lorsque vous utilisez hello outil d’importation/exportation Azure et comment toohandle les."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 5445cefe2703edf4d9d285f761433b7b66d8cb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a>Résolution des problèmes de hello outil d’importation/exportation Azure
Hello, outil de Microsoft Azure Import/Export renvoie des messages d’erreur s’il rencontre des problèmes. Cette rubrique répertorie certains des problèmes courants que les utilisateurs peuvent rencontrer.  
  
## <a name="a-copy-session-fails-what-i-should-do"></a>Une session de copie échoue, que faire ?  
 Lorsqu’une session de copie échoue, il existe deux possibilités :  
  
 Si l’erreur de hello est renouvelable, par exemple, si le partage de réseau hello était hors connexion pour une courte période et maintenant est en ligne, vous pouvez reprendre la session de copie hello. Si l’erreur de hello n’est pas renouvelable, par exemple, si vous avez spécifié un répertoire du fichier source incorrect hello dans les paramètres de ligne de commande hello, vous devez la session de copie tooabort hello. Consultez la page [Préparer des disques durs pour un travail d’importation](storage-import-export-tool-preparing-hard-drives-import-v1.md) pour plus d’informations sur la reprise et l’abandon de sessions de copie.  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a>Je n’arrive pas à reprendre ou à abandonner une session de copie.  
 Si la session de copie hello est hello première session de copie pour un lecteur, message d’erreur hello doit indiquer : « hello première session de copie ne peut pas être repris ou abandonnée. » Dans ce cas, vous pouvez supprimer l’ancien fichier journal de hello et réexécutez la commande hello.  
  
 Si une session de copie n’est pas hello un premier pour un lecteur, il peut toujours être repris ou abandonnée.  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a>J’ai perdu le fichier journal de hello, est-il possible de créer le travail de hello ?  
 fichier de journal Hello pour un lecteur contient des informations complètes de hello de la copie du lecteur de données toothis, et il est nécessaire tooadd plus lecteur toohello de fichiers et sera toocreate utilisé un travail d’importation. Si le fichier journal de hello est perdu, vous devez tooredo toutes les sessions de copie hello pour le lecteur de hello.  
  
## <a name="next-steps"></a>Étapes suivantes
 
* [Configuration de l’outil d’importation/exportation azure hello](storage-import-export-tool-setup-v1.md)   
* [Préparation des disques durs pour un travail d’importation](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Consultation de l’état du travail avec les fichiers journaux de copie](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Réparation d’un travail d’importation](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Réparation d’un travail d’exportation](storage-import-export-tool-repairing-an-export-job-v1.md)
