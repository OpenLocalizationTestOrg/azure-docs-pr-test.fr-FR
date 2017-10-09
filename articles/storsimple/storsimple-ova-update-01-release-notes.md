---
title: "notes de publication de mises à jour de tableau virtuel aaaStorSimple | Documents Microsoft"
description: "Décrit les problèmes critiques en suspens et résolutions pour hello StorSimple Virtual Array mise à jour, 0,2 et 0,1 en cours d’exécution."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3993864d-2ddd-4302-a2f1-8d737fba6eab
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2016
ms.author: alkohli
ms.openlocfilehash: dfd38890feeb667c95134f2adbb35ce2df165620
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-virtual-array-update-02-and-01-release-notes"></a>Notes de publication de StorSimple Virtual Array Update 0.2 et 0.1
## <a name="overview"></a>Vue d'ensemble
Bonjour notes de publication suivantes identifient les problèmes critiques en suspens hello et hello problèmes résolus pour les mises à jour de Microsoft Azure StorSimple Virtual Array. (Microsoft Azure StorSimple Virtual Array est également appelé un appareil virtuel hello StorSimple local ou un appareil virtuel StorSimple hello.) 

notes de publication Hello sont mis à jour, et que les problèmes critiques nécessitant une solution de contournement sont découverts, ils sont ajoutés. Avant de déployer votre appareil virtuel StorSimple, lisez attentivement les informations de hello contenues dans les notes de publication hello.

Mise à jour 0,2 correspond la version du logiciel toohello **10.0.10280.0**; Mise à jour 0.1 est version **10.0.10279.0**. sections de Hello ci-dessous répertorient les modifications hello pour chaque mise à jour. 

> [!NOTE]
> Les mises à jour entraînent des perturbations et redémarrent votre appareil. Si les e/s sont en cours d’exécution, les appareils hello entraîne un temps d’arrêt.
> 
> 

## <a name="issues-fixed-in-hello-update-02"></a>Problèmes résolus dans hello mise à jour 0,2
Mise à jour 0,2 inclut toutes les modifications à partir de la mise à jour 0.1 addition toohello correctif est décrit dans hello tableau suivant :

| Fonctionnalité | Problème |
| --- | --- |
| Mises à jour |Dans la dernière version de hello, les mises à jour n’ont pas été détectées automatiquement Bonjour portail Azure classic, afin de vous aviez toouse hello tooinstall l’interface utilisateur Web locales des mises à jour. Ce problème a été résolu dans cette version. Après avoir installé la mise à jour 0,2, vous pouvez installer des mises à jour ultérieures à l’aide de hello portail Azure classic. |

## <a name="whats-new-in-hello-update-01"></a>Nouveautés de hello mise à jour 0.1
Mise à jour 0.1 contient des éléments suivants de hello correctifs de bogues et améliorations. 

* **Résilience améliorée pour les pannes de cloud**: cette version comporte plusieurs correctifs de bogues autour de la récupération d’urgence, la sauvegarde, la restauration et la hiérarchisation dans les cas de hello d’une interruption de la connectivité cloud. 
* **Amélioration des performances de restauration**: cette version comporte des correctifs de bogues qui ont considérablement réduire le temps d’exécution hello hello de travaux de restauration.
* **Automatisée de l’optimisation de récupération de l’espace**: lors de la suppression des données dans les volumes alloués, hello stockage inutilisés les blocs doivent toobe récupéré. Cette version comporte des processus de récupération d’espace hello améliorée du cloud hello entraîne hello inutilisé espace devenant plus rapidement que comparés toohello versions précédentes disponibles.
* **Nouvelles images de disque virtuel**: nouveau disque dur virtuel, VHDX et VMDK sont désormais disponibles via hello portail Azure classic. Vous pouvez télécharger ces images tooprovision nouvelle mise à jour 0.1 des appareils.
* **Améliorer la précision de hello de l’état de travaux dans le portail de hello**: Bonjour une version antérieure du logiciel, l’état du travail reporting dans le portail de hello n’était pas précise. Ce problème a été résolu dans cette version.
* **Expérience de jointure de domaine**: correctifs de bogues liés toodomain jonction et le changement de nom du périphérique de hello.

## <a name="issues-fixed-in-hello-update-01"></a>Problèmes résolus dans hello mise à jour 0.1
Hello tableau suivant fournit un résumé des problèmes résolus dans cette version.

| Non. | Fonctionnalité | Problème |
| --- | --- | --- |
| 1 |VMDK |Dans certaines versions de VMware, les disques du système d’exploitation hello a été considéré comme à l’origine des alertes et interrompre les opérations normales. Ce problème a été résolu dans cette version. |
| 2 |Serveur iSCSI |Dans la dernière version de hello, utilisateur de hello a été requise toospecify une passerelle pour chaque interface réseau activée de votre appareil virtuel StorSimple. Ce comportement est modifié dans cette version afin que l’utilisateur hello a tooconfigure au moins une passerelle pour toutes les interfaces réseau de hello activée. |
| 3 |Package de prise en charge |Dans l’hello une version antérieure du logiciel, prennent en charge de la collection de packages a échoué lors de la taille de lot de hello a été supérieure à 1 Go. Ce problème a été résolu dans cette version. |
| 4 |Accès au cloud |Dernière version de hello, si hello StorSimple Virtual Array n’avait pas de connectivité réseau et a été redémarré, hello d’interface utilisateur locale vous avez des problèmes de connectivité. Ce problème a été résolu dans cette version. |
| 5 |Graphiques de surveillance |Dans la version précédente de hello, après un basculement de l’appareil, graphiques de l’utilisation de capacité de cloud hello affichent des valeurs incorrectes dans hello portail Azure classic. Il est résolu dans la version actuelle de hello. |

## <a name="known-issues-in-hello-update-01"></a>Problèmes connus dans hello mise à jour 0.1
Bonjour tableau suivant fournit un résumé des problèmes connus de hello StorSimple Virtual Array et inclut des problèmes hello indication mise en production à partir de versions précédentes de hello. **Hello version problèmes indiquée dans cette version sont marquées par un astérisque. Presque tous les problèmes de hello dans cette liste ont un report de version de hello disponibilité générale de StorSimple Virtual Array.**

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
| **14.** |Serveur de fichiers* |Si un fichier dans un dossier a un autre flux de données (ADS) associé, hello annonces n’est pas sauvegardé ou restauré via la récupération d’urgence, de clonage et de récupération au niveau de l’élément. | |

## <a name="next-step"></a>Étape suivante
[Installation de mises à jour](storsimple-ova-install-update-01.md) sur votre instance StorSimple Virtual Array.

