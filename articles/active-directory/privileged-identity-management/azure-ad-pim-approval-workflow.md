---
title: "workflows d’approbation de la gestion Privileged Identity aaaAzure | Documents Microsoft"
description: "En savoir plus sur les flux de travail d’approbation dans Privileged Identity Management (PIM)"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 4afaf5c138798a803eb3d3b7905b9361d65792cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="approvals-preview"></a>Approbations (version préliminaire)

## <a name="overview"></a>Vue d'ensemble

Avec des approbations pour Privileged Identity Management, vous pouvez configurer l’approbation toorequire rôles pour l’activation et choisissez un ou plusieurs utilisateurs ou groupes approbateurs comme délégués. Poursuivez votre lecture toolearn comment tooconfigure rôles et de sélectionner les approbateurs.

>[!NOTE]
N’oubliez pas que cette fonctionnalité est en cours de développement et que vous pouvez rencontrer des bugs. fonctionnalité de Hello, y compris le texte et les conventions d’affectation de noms sont susceptibles de changer et ne doivent pas être considérés finales.


## <a name="key-terminology"></a>Terminologie clé

*Utilisateur rôle éligible* – un utilisateur éligible rôle est un utilisateur au sein de votre organisation qui a été attribué rôle tooan Azure AD comme éligibles (rôle nécessite l’activation).

*Approbateur délégué* : un approbateur délégué est une ou plusieurs personnes ou groupes au sein de votre Azure AD responsables de l’approbation des demandes d’activation de rôle.

## <a name="scenarios"></a>Scénarios

version préliminaire limitée de Hello prend en charge hello les scénarios suivants :

**En tant qu’Administrateur de rôle privilégié (PRA), vous pouvez :**

-   [activer l’approbation pour des rôles spécifiques](#enable-approval-for-specific-roles)

-   [spécifier les demandes de tooapprove les utilisateurs et/ou groupes approbateur](#specify-approver-users-and/or-groups-to-approve-requests)

-   [afficher l’historique des demandes et approbations pour tous les rôles privilégiés](#view-request-and-approval-history-for-all-privileged-roles)

**En tant d’approbateur désigné, vous pouvez :**

-   [afficher les approbations (demandes) en attente](#view-pending-approvals-requests)

-   [approuver ou rejeter des demandes d’élévation de rôle (unique et/ou en bloc)](#approve-or-reject-requests-for-role-elevation-single-and/or-bulk)

-   [justifier mon approbation/rejet](#provide-justification-for-my-approval/rejection) 

**En tant qu’un utilisateur de rôle éligible, vous pouvez :**

-   [demander l’activation d’un rôle qui nécessite une approbation](#request-activation-of-a-role-that-requires-approval)

-   [afficher l’état de votre demande de tooactivate hello](#view-the-status-of-your-request-to-activate)

-   [exécuter la tâche dans Azure AD si l’activation a été approuvée](#complete-your-task-in-azure-ad-if-activation-was-approved)

### <a name="navigation"></a>Navigation

Nous avons mis à jour les approbations de hello navigation toosupport

![](media/azure-ad-pim-approval-workflow/image001.png)

page d’accueil par défaut Hello fournit tooinformation un accès aisé à propos de PIM et hello nouvelle documentation approbations.

![](media/azure-ad-pim-approval-workflow/image002.png)

Nous avons également ajouté une nouvelle section pour tous les utilisateurs de PIM, « Mon historique d’audit ». Vous trouverez ici identité de tooyour applique toutes les hello plus d’informations. Cela inclut toutes les demandes en attente et terminées, les décisions sur les demandes hello vous résolvez et toutes vos activations rôle passées dans un emplacement pratique.

![](media/azure-ad-pim-approval-workflow/image003.png)

### <a name="enable-approval-for-specific-roles"></a>Activer l’approbation pour des rôles spécifiques

approbation tooenable pour un rôle spécifique, sélectionnez tout d’abord les rôles d’annuaire à partir du volet de navigation gauche hello.

![](media/azure-ad-pim-approval-workflow/image004.png)

Recherchez et sélectionnez Paramètres Bonjour de navigation gauche des rôles d’annuaire

![](media/azure-ad-pim-approval-workflow/image006.png)

Sélectionner des rôles privilégiés :

![](media/azure-ad-pim-approval-workflow/image009.png)

Sélectionnez « Activer » Bonjour nécessitent la section sur l’approbation :

![](media/azure-ad-pim-approval-workflow/image011.png)

Une fois activé, panneau de hello développera hello tooshow les détails suivants :

![](media/azure-ad-pim-approval-workflow/image013.png)

>[!NOTE]
Si vous n’effectuez pas spécifiez des approbateurs, hello PRA(s) devenir l’ou les approbateurs hello par défaut. PRA(s) serait requise tooapprove d’activation de toutes les demandes de ce rôle.

### <a name="specify-approver-users-andor-groups-tooapprove-requests"></a>Spécifier les demandes de tooapprove les utilisateurs et/ou groupes approbateur

toodelegate approbation, cliquez sur hello option trop « sélectionner les approbateurs » :

![](media/azure-ad-pim-approval-workflow/image015.png)

Lors du chargement de panneau d’approbateurs sélectionnez hello, vous pouvez rechercher un utilisateur spécifique ou un groupe à l’aide de la barre de recherche hello en haut de hello ou en sélectionnant dans la liste prédéfinie de hello, puis cliquez sur « Select » une fois :

![](media/azure-ad-pim-approval-workflow/image017.png)

Remarque : vous pouvez sélectionner plusieurs utilisateurs ou groupes à la fois.

La sélection apparaît dans la liste hello des approbateurs sélectionnés comme indiqué ci-dessous :

![](media/azure-ad-pim-approval-workflow/image019.png)

tooremove un approbateur, cliquez simplement sur le nom de tootheir suivant hello Remove bouton.

approbateurs supplémentaires tooadd, processus de répétition hello.

## <a name="view-request-and-approval-history-for-all-privileged-roles"></a>Afficher l’historique des demandes et approbations pour tous les rôles privilégiés

l’historique de demande et d’approbation tooview pour tous les rôles privilégiés, sélectionnez l’historique d’Audit à partir du tableau de bord hello :

![](media/azure-ad-pim-approval-workflow/image021.png)

>[!NOTE]
Vous pouvez trier les données de salutation par Action et recherchez « Activation approuvé »

### <a name="view-pending-approvals-requests"></a>Afficher les approbations (demandes) en attente

En tant qu’approbateur délégué, vous recevez une notification par courrier électronique lorsqu’une demande est en attente d’approbation. tooview ces demandes dans le portail PIM hello, depuis l’onglet tableau de bord (dans une nouvelle navigation hello) sélectionnez hello » en attente demandes d’approbation » hello la barre de navigation gauche.

![](media/azure-ad-pim-approval-workflow/image023.png)

Une liste des demandes d’approbation en attente s’affiche ici :

![](media/azure-ad-pim-approval-workflow/image024.png)

### <a name="approve-or-reject-requests-for-role-elevation-single-andor-bulk"></a>Approuver ou rejeter des demandes d’élévation de rôle (unique et/ou en bloc)

Vous souhaitez tooapprove ou refusez les demandes de hello, puis cliquez sur le bouton hello dans la barre d’action qui correspond à votre décision :

![](media/azure-ad-pim-approval-workflow/image025.png)

### <a name="provide-justification-for-my-approvalrejection"></a>Justifier mon approbation/rejet

Cela ouvre une nouvelle tooapprove de panneau ou refuser plusieurs demandes à la fois. Entrer une justification de votre choix et cliquez sur Approuver (ou refuser) au bas de hello ou panneau de hello :

![](media/azure-ad-pim-approval-workflow/image029.png)

Lorsque le processus de demande de hello est terminée, symbole d’état hello reflète la décision (dans cet exemple, la décision de hello est approuver) :

![](media/azure-ad-pim-approval-workflow/image031.png)

### <a name="request-activation-of-a-role-that-requires-approval"></a>Demander l’activation d’un rôle qui nécessite une approbation

Demander l’activation d’un rôle qui nécessite l’approbation peut être lancée à partir de la navigation de PIM ancien hello, ou d’une nouvelle navigation hello, en tant que processus hello pour le reste de l’activation de rôle hello identiques. Il suffit de sélectionner un rôle à partir de la liste de hello des rôles pour activer :

![](media/azure-ad-pim-approval-workflow/image033.png)

Si un rôle de privilège requiert Multi-Factor Authentication, vous êtes invité à effectuer la tâche suivante en premier :

![](media/azure-ad-pim-approval-workflow/image035.png)

Lorsque vous avez terminé, cliquez sur Activer et entrez une justification (si nécessaire) :

![](media/azure-ad-pim-approval-workflow/image037.png)

demandeur de Hello s’affiche une notification indiquant que hello demande en attente d’approbation :

![](media/azure-ad-pim-approval-workflow/image039.png)

### <a name="view-hello-status-of-your-request-tooactivate"></a>Afficher l’état de votre demande de tooactivate hello

Affichage de l’état de hello d’une demande en attente de tooactivate doit être accessible à partir de la nouvelle navigation. À partir de la barre de navigation gauche hello, sélectionnez l’onglet de « Mes demandes » hello :

![](media/azure-ad-pim-approval-workflow/image041.png)

état de la demande Hello par défaut est trop « « en attente », mais vous pouvez basculer toosee tous les ou refuser les demandes.

### <a name="complete-your-task-in-azure-ad-if-activation-was-approved"></a>Exécuter la tâche dans Azure AD si l’activation a été approuvée

Une fois que hello demande est approuvée, rôle de hello est actif et vous pouvez continuer avec n’importe quel travail qui requiert ce rôle.

![](media/azure-ad-pim-approval-workflow/image043.png)

## <a name="next-steps"></a>Étapes suivantes

Vos commentaires nous sont précieux toous. Vous pouvez tooshare libre commentaires ou des commentaires nous ici !
