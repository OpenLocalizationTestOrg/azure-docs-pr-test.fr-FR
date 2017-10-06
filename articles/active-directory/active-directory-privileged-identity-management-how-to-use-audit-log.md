---
title: "journal d’audit aaaHow toouse hello dans Azure AD Privileged Identity Management | Documents Microsoft"
description: "Découvrez comment du journal d’audit de toouse hello dans l’extension d’Azure Privileged Identity Management hello."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 5d13a6dd-1fcb-4e76-82fb-cb2f4f0e4357
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 36987eaab9fe02c5dd7b4f4705e487299430745d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-audit-log-in-pim"></a>À l’aide du journal d’audit de hello dans PIM
Vous pouvez utiliser toosee de journal d’audit hello Privileged Identity Management (PIM) toutes les affectations d’utilisateur de hello et des activations sur une période donnée. Si vous souhaitez que l’historique d’audit de hello toosee d’activité de votre client, y compris l’administrateur, utilisateur final et l’activité de synchronisation, vous pouvez utiliser hello [rapports d’accès et d’utilisation de Azure Active Directory.](active-directory-view-access-usage-reports.md)

## <a name="navigate-toohello-audit-log"></a>Parcourir le journal d’audit de toohello
À partir de hello [portail Azure](https://portal.azure.com) tableau de bord, sélectionnez hello **Azure AD Privileged Identity Management** application. À partir de là, vous pouvez accéder au journal d’audit de hello en cliquant sur **gérer les rôles privilégiés** > **historique d’Audit** dans le tableau de bord hello PIM.

## <a name="hello-audit-log-graph"></a>graphique de journal d’audit Hello
Vous pouvez utiliser des activations totales hello du tooview journal hello audit activations maximales par jour et des activations moyenne par jour dans un graphique linéaire.  Vous pouvez également filtrer les données de salutation par rôle, s’il existe plusieurs rôles dans l’historique d’audit de hello.

Hello d’utilisation **temps**, **action**, et **rôle** boutons toosort hello journal.

## <a name="hello-audit-log-list"></a>liste des journaux d’audit Hello
les colonnes dans la liste des journaux d’audit hello Hello sont :

* **Demandeur** -utilisateur hello qui a demandé l’activation de rôles hello ou de modification.  Si la valeur de hello est « Système Azure », consultez le journal d’audit Azure hello pour plus d’informations.
* **Utilisateur** -utilisateur hello est activation ou tooa de rôle.
* **Rôle** -rôle de hello attribuée ou activée par l’utilisateur de hello.
* **Action** - actions hello pris par le demandeur de hello. Ceci peut inclure l'attribution, la non-attribution, l’activation ou la désactivation.
* **Heure** : lors de l’action de hello s’est produite.
* **Raisonnement** -si n’importe quel texte a été entré dans le champ reason du hello lors de l’activation, il s’affiche ici.
* **Expiration** : concerne uniquement l’activation de rôles.

## <a name="filter-hello-audit-log"></a>Filtrer le journal d’audit hello
Vous pouvez filtrer les informations de hello qui s’affiche dans le journal d’audit de hello en cliquant sur hello **filtre** bouton.  Hello **Panneau de paramètres de mise à jour graphique** s’affiche.

Une fois que vous définissez des filtres de hello, cliquez sur **mise à jour** toofilter les données de salutation dans le journal de hello.  Si les données de salutation n’apparaissent pas immédiatement, actualisez la page de hello.

### <a name="change-hello-date-range"></a>Modifier la plage de dates hello
Hello d’utilisation **aujourd'hui**, **semaine**, **mois**, ou **personnalisé** boutons période toochange hello du journal d’audit de hello.

Lorsque vous choisissez hello **personnalisé** bouton, vous aurez un **de** champ date et un **à** date champ toospecify une plage de dates pour le journal de hello.  Vous pouvez entrer des dates de hello dans le format MM/JJ/AAAA ou cliquez sur hello **calendrier** icône et choisir la date de hello dans un calendrier.

### <a name="change-hello-roles-included-in-hello-log"></a>Modifier les rôles hello inclus dans le journal de hello
Activez ou désactivez hello **rôle** tooinclude rôle tooeach suivant de case à cocher ou les exclure de hello ouvrir une session.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

