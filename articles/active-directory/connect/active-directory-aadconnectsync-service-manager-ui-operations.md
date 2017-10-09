---
title: "Opérations d’Azure AD Connect Synchronization Service Manager | Microsoft Docs"
description: "Comprendre l’onglet opérations hello hello Synchronization Service Manager pour Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
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
ms.openlocfilehash: decbc53613d456a71cd116c40c5e1fd761efd4af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-sync-service-manager-operations-tab"></a>À l’aide de hello onglet opérations du Gestionnaire de Service de synchronisation

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/operations.png)

onglet d’opérations Hello montre les résultats de hello des opérations les plus récentes de hello. Cet onglet est toounderstand clé et résoudre les problèmes.

## <a name="understand-hello-information-visible-in-hello-operations-tab"></a>Comprendre les informations hello visibles dans l’onglet opérations de hello
moitié supérieure de Hello affiche toutes les séries dans l’ordre chronologique. Par défaut, journal des opérations hello conserve les informations relatives hello sept derniers jours, mais ce paramètre peut être modifié par hello [planificateur](active-directory-aadconnectsync-feature-scheduler.md). Vous souhaitez toolook pour une exécution qui n’affiche pas un état de réussite. Vous pouvez modifier hello tri en cliquant sur les en-têtes hello.

Hello **état** colonne est informations les plus importantes hello et montre hello plus grave problème pour une exécution. Voici un résumé des États de hello plus courantes dans l’ordre de priorité tooinvestigate (où * indiquer plusieurs chaînes d’erreur possible).

| État | Commentaire |
| --- | --- |
| stopped-* |Hello exécuter n’a pas pu se terminer. Par exemple, si hello système distant est arrêté et ne peut pas être contacté. |
| stopped-error-limit |Il existe plus de 5 000 erreurs. Hello exécuter a été automatiquement arrêté en raison de toohello un grand nombre d’erreurs. |
| completed-\*-errors |Hello exécution, mais il existe des erreurs (moins de 5 000) qui doivent être examinés. |
| completed-\*-warnings |Hello exécution terminée, mais certaines données ne sont pas en état de hello attendu. Si vous avez des erreurs, alors ce message n’est, en général, qu’un symptôme. N’examinez pas les avertissements avant d’avoir résolu les erreurs. |
| réussi |Aucun problème. |

Lorsque vous sélectionnez une ligne, en bas de hello met à jour les détails de hello tooshow de qui s’exécutent. toohello à gauche de la partie inférieure de hello, vous disposez d’un message de la liste **étape #**. Cette liste ne s’affiche que si votre forêt contient plusieurs domaines et que chaque domaine est représenté par une étape. nom de domaine Hello se trouve sous le titre de hello **Partition**. Sous **statistiques de synchronisation**, vous pouvez trouver plus d’informations sur le nombre de hello de modifications qui ont été traités. Vous pouvez cliquer sur hello liens tooget une liste d’objets de hello modifié. Si vous avez des objets comportant des erreurs, celles-ci s’affichent sous **Erreurs de synchronisation**.

Pour plus d’informations, consultez [Dépanner un objet qui bloque la synchronisation](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md)

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuration.

En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
