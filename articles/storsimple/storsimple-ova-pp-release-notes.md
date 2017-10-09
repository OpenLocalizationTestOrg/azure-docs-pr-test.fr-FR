---
title: "Notes de mise à jour du tableau virtuel aaaStorSimple | Documents Microsoft"
description: "Décrit les problèmes critiques en suspens et résolutions pour hello StorSimple Virtual Array."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 84908160-2b8b-4f4f-a674-f39aaa0bd4de
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/13/2016
ms.author: alkohli
ms.openlocfilehash: ca7b543f95cf5787b7fef39f53887161ebfa7fcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-release-notes"></a>Notes de publication pour StorSimple Virtual Array
## <a name="overview"></a>Vue d'ensemble
Hello notes de publication suivantes identifient les problèmes critiques ouverts hello pour cette version de la disponibilité générale (GA) mars 2016 hello Hello Microsoft Azure StorSimple Virtual Array (également appelé un appareil virtuel StorSimple local de hello ou hello virtuel StorSimple APPAREIL). Cette version correspond toosoftware version 10.0.10271.0.

notes de publication Hello sont mis à jour, et que les problèmes critiques nécessitant une solution de contournement sont découverts, ils sont ajoutés. Avant de déployer votre appareil virtuel StorSimple, lisez attentivement les informations de hello contenues dans les notes de publication hello. 

Hello tableau suivant fournit un résumé des problèmes connus dans cette version.

| Non. | Fonctionnalité | Problème | Solution de contournement/commentaires |
| --- | --- | --- | --- |
| **1.** |Mises à jour |les périphériques virtuels Hello créés dans la version préliminaire de hello ne peut pas être la version disponibilité générale de mise à jour tooa pris en charge. |Ces périphériques virtuels doivent être basculés pour hello version disponibilité générale à l’aide d’un flux de travail de récupération d’urgence. |
| **2.** |Disque de données configuré |Une fois, vous avez configuré un disque de données d’une certaine taille spécifiée et créé hello correspondant un appareil virtuel StorSimple, vous ne devez pas développer ou réduire disque de données hello. Tentative de toodo entraînerait une perte de toutes les données hello dans les niveaux de hello local de l’appareil de hello. | |
| **3.** |Stratégie de groupe |Quand un appareil est joint au domaine, appliquer une stratégie de groupe peut nuire opération de périphérique hello. |Assurez-vous que votre tableau virtuel est dans sa propre unité d’organisation (UO) pour Active Directory et aucun objet de stratégie de groupe (GPO) n’est appliqué tooit. |
| **4.** |Interface utilisateur web locale |Si les fonctionnalités de sécurité améliorées sont activées dans Internet Explorer (IE ESC), certaines pages de l’interface utilisateur web locale, comme Dépannage ou Maintenance, peuvent ne pas fonctionner correctement. Les boutons sur ces pages peuvent également ne pas fonctionner. |Désactivez les fonctionnalités de sécurité améliorées d'Internet Explorer. |
| **5.** |Interface utilisateur web locale |Sur un ordinateur virtuel Hyper-V, hello interfaces réseau dans web hello l’interface utilisateur sont affichés sous la forme d’interfaces de 10 Gbits/s. |Ce comportement est le reflet de Hyper-V. Hyper-V affiche toujours 10 Gbits/s pour les cartes de réseau virtuel. |
| **6.** |Partages ou volumes à plusieurs niveaux |Plage d’octets pour les applications qui fonctionnent avec hello StorSimple volumes hiérarchisés de verrouillage n’est pas pris en charge. Si le verrouillage de la plage d'octets est activé, la hiérarchisation StorSimple ne fonctionnera pas. |Mesures recommandées :  <br></br>Désactivez le verrouillage de plage d'octets dans la logique de votre application.<br></br>Choisissez tooput les données pour cette application dans les volumes attachés localement par opposition tootiered volumes.<br></br>*Avertissement*: si à l’aide locale épinglée de volumes et verrouillage de plage d’octets est activé, sachez que les volumes hello attaché localement peuvent être en ligne avant même que la restauration hello est terminée. Dans ce cas, si une restauration est en cours, puis vous devez attendre hello restauration toocomplete. |
| **7.** |Partages à plusieurs niveaux |L'utilisation de fichiers volumineux peut entraîner montée en charge de niveau lente. |Lorsque vous travaillez avec des fichiers volumineux, nous vous recommandons de que ce fichier le plus volumineux hello est inférieur à 3 % de la taille du partage hello. |
| **8.** |Capacité utilisée pour les partages |Vous pouvez voir partager la consommation en absence de hello de toutes les données sur le partage de hello. Il s’agit, car la capacité hello utilisé pour les partages inclut des métadonnées. | |
| **9.** |Récupération d'urgence |Vous ne pouvez effectuer la récupération d’urgence hello d’un toohello de serveur de fichier même domaine que celui de l’appareil source de hello. Appareil de cible de tooa de récupération d’urgence dans un autre domaine n’est pas pris en charge dans cette version. |Ceci sera implémenté dans une version ultérieure. |
| **10.** |Azure PowerShell |périphériques virtuels StorSimple de Hello ne peut pas être gérés via hello Azure PowerShell dans cette version. |Toute la gestion de périphériques virtuels de hello hello doit être effectuée via hello portail Azure classic et web locale de hello l’interface utilisateur. |
| **11.** |Modification de mot de passe |console de l’appareil virtuel tableau Hello accepte uniquement les entrées au format de clavier en-US. | |
| **12.** |CHAP |Il est impossible de supprimer les informations d’identification CHAP une fois qu’elles ont été créées. En outre, si vous modifiez les informations d’identification de hello CHAP, vous devez tootake des volumes hello en mode hors connexion, puis les mettre en ligne pour modifier un effet de tootake hello. |Ceci sera résolu dans une version ultérieure. |
| **13.** |Serveur iSCSI |Hello utilisé le stockage affiché pour un volume iSCSI peut être différent dans le service StorSimple Manager hello et hôte iSCSI de hello. |ordinateur hôte iSCSI de Hello possède la vue de système de fichiers de hello.<br></br>Appareil de Hello voit blocs hello allouées lorsque le volume de hello était à la taille maximale de hello. |

