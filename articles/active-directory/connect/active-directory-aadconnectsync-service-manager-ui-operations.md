---
title: "Opérations d’Azure AD Connect Synchronization Service Manager | Microsoft Docs"
description: "Comprendre l’onglet des opérations dans Synchronization Service Manager pour Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: 
ms.assetid: 97a26565-618f-4313-8711-5925eeb47cdc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 91210edc3306b834cbd68f0f028845a7f36dd0b5
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/18/2018
---
# <a name="using-the-sync-service-manager-operations-tab"></a>Utilisation de l’onglet Opérations de Sync Service Manager

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

L’onglet des opérations affiche les résultats des opérations les plus récentes. Cet onglet est essentiel pour comprendre et résoudre les problèmes.

## <a name="understand-the-information-visible-in-the-operations-tab"></a>Comprendre les informations visibles dans l’onglet des opérations
La partie supérieure affiche toutes les exécutions dans un ordre chronologique. Par défaut, le journal des opérations conserve les informations des sept derniers jours, mais vous pouvez modifier ce paramètre à l’aide du [planificateur](active-directory-aadconnectsync-feature-scheduler.md). Vous souhaitez rechercher toute exécution qui ne présente pas un état de réussite. Vous pouvez modifier le tri en cliquant sur les en-têtes.

La colonne **État** regroupe les informations les plus importantes et présente le problème le plus sévère pour une exécution. Voici un récapitulatif rapide des états les plus courants par ordre de priorité d’inspection (où * indique plusieurs chaînes d’erreur possibles).

| Statut | Commentaire |
| --- | --- |
| stopped-* |L’exécution n’a pas pu se terminer. Par exemple, si le système distant est arrêté et ne peut pas être contacté. |
| stopped-error-limit |Il existe plus de 5 000 erreurs. L’exécution a été automatiquement arrêtée en raison du grand nombre d’erreurs. |
| completed-\*-errors |L’exécution s’est terminée, mais il existe des erreurs (moins de 5 000) qui doivent être examinées. |
| completed-\*-warnings |L’exécution s’est terminée, mais des données ne sont pas dans l’état attendu. Si vous avez des erreurs, alors ce message n’est, en général, qu’un symptôme. N’examinez pas les avertissements avant d’avoir résolu les erreurs. |
| réussi |Aucun problème. |

Lorsque vous sélectionnez une ligne, la partie inférieure est mise à jour pour afficher les détails de cette exécution. À l’extrême gauche de la partie inférieure, une liste peut s’afficher indiquant **Step #**. Cette liste ne s’affiche que si votre forêt contient plusieurs domaines et que chaque domaine est représenté par une étape. Le nom de domaine se trouve sous le titre **Partition**. Sous **Statistiques de synchronisation**, vous trouverez plus d’informations sur le nombre de modifications qui ont été traitées. Vous pouvez cliquer sur les liens pour obtenir la liste des objets modifiés. Si vous avez des objets comportant des erreurs, celles-ci s’affichent sous **Erreurs de synchronisation**.

Pour plus d’informations, consultez [Dépanner un objet qui bloque la synchronisation](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)

## <a name="next-steps"></a>étapes suivantes
En savoir plus sur la configuration de la [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) .

En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
