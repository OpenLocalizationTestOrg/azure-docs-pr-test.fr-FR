---
title: "limitations de Cloud Shell (version préliminaire) aaaAzure | Documents Microsoft"
description: "Vue d’ensemble des limites d’Azure Cloud Shell"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a>Limitations d’Azure Cloud Shell
Azure Cloud Shell a suivant hello restrictions connues :

## <a name="system-state-and-persistence"></a>État du système et persistance
ordinateur Hello qui fournit votre session d’interpréteur de commandes de Cloud est temporaire et il est recyclé une fois votre session est inactive pendant 20 minutes. Cloud Shell nécessite une toobe de partage de fichiers monté. Par conséquent, votre abonnement doit être en mesure de tooset des tooaccess de ressources de stockage Cloud Shell. Autres éléments à prendre en compte :
* Avec le stockage monté, seules les modifications apportées à votre répertoire `$Home` ou `clouddrive` sont conservées.
* Les partages de fichiers peuvent être montés uniquement depuis votre [région affectée](persisting-shell-storage.md#mount-a-new-clouddrive).
* Azure Files prend uniquement en charge les comptes de stockage localement redondant et les comptes de stockage géoredondant.

## <a name="user-permissions"></a>Autorisations utilisateur
Les autorisations sont définies en tant qu’utilisateurs standards sans accès sudo. Les installations en dehors du répertoire `$Home` ne sont pas conservées.
Bien que certaines commandes de hello `clouddrive` répertoire comme `git clone`, n’ont pas les autorisations appropriées, votre `$Home` active dispose des autorisations appropriées.

## <a name="browser-support"></a>Prise en charge des navigateurs
Cloud Shell prend en charge les versions les plus récentes de Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox et Apple Safari hello. Safari en mode privé n’est pas pris en charge.

## <a name="copy-and-paste"></a>Copier et coller
CTRL + C et Ctrl + V ne fonctionnent pas comme copier/coller raccourcis dans le Cloud Shell sur des ordinateurs Windows, utilisez Ctrl + Inser et MAJ + INSER toocopy et collez respectivement.

Avec le bouton Copier-coller options sont également disponibles, mais avec le bouton fonction est un accès au Presse-papiers de toobrowser spécifiques sujet.

## <a name="editing-bashrc"></a>Modifier .bashrc
Faites attention lorsque vous modifiez .bashrc : cela peut entraîner des erreurs inattendues dans Cloud Shell.

## <a name="bashhistory"></a>.bash_history
Votre historique de commandes de l’interpréteur de commandes risque d’être incohérent en raison d’interruptions de sessions Cloud Shell ou de sessions simultanées.

## <a name="usage-limits"></a>Limites d’utilisation
Cloud Shell est destiné aux cas d’usage interactif. De fait, les sessions non interactives longues se terminent sans avertissement.

## <a name="network-connectivity"></a>Connectivité réseau
Aucun temps d’attente dans un environnement de Cloud est connecté à internet toolocal sujet, Cloud Shell continue toocarry tooattempt les instructions envoyées.

## <a name="next-steps"></a>Étapes suivantes
[Démarrage rapide de Cloud Shell](quickstart.md)
