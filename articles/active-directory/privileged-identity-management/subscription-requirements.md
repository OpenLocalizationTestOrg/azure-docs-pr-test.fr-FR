---
title: "abonnements de la gestion des identités aaaPrivileged - Azure | Documents Microsoft"
description: "Explique les abonnement hello et en matière de gestion et à l’aide d’Azure AD Privileged Identity Management dans votre client de licence"
services: active-directory
documentationcenter: 
author: barclayn
manager: mbaldwin
editor: mwahl
ms.assetid: 34367721-8b42-4fab-a443-a2e55cdbf33d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: barclayn
ms.custom: pim
ms.openlocfilehash: 2639d13c250a582fdcf0b277c9bab37fdfcabcb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-privileged-identity-management-subscription-requirements"></a>Exigences en matière d’abonnement d’Azure AD Privileged Identity Management

Azure AD Privileged Identity Management est disponible dans le cadre de l’édition hello Premium P2 d’Azure AD. Pour plus d’informations sur hello autres fonctionnalités de P2 et le compare tooPremium P1, consultez [éditions Azure Active Directory](../active-directory-editions.md).

>[!NOTE]
Lorsque Azure Active Directory (Azure AD) Privileged Identity Management a été dans l’aperçu, ne comportaient aucune vérification de la licence pour un service de hello tootry client.  Maintenant que Azure AD Privileged Identity Management a atteint la disponibilité générale, un abonnement d’évaluation ou payant doit être présent pour hello toocontinue de client à l’aide de Privileged Identity Management après décembre 2016.
  

## <a name="confirm-your-trial-or-paid-subscription"></a>Confirmer votre abonnement d’évaluation ou payant

Si vous ne savez pas si votre organisation dispose d’une version d’évaluation ou l’abonnement, vous pouvez vérifier s’il existe un abonnement de votre client à l’aide des commandes hello inclus dans Azure Active Directory Module pour Windows PowerShell V1. 
1. Ouvrez une fenêtre PowerShell.
2. Entrez `Connect-MsolService` tooauthenticate en tant qu’utilisateur dans votre client.
3. Entrez `Get-MsolSubscription | ft SkuPartNumber,IsTrial,Status`.

Cette commande récupère une liste d’abonnements hello dans votre client. S’il y a qu'aucuns lignes ne retourné, que vous devez la version d’évaluation tooobtain un P2 Azure AD Premium, achetez un abonnement de Azure AD Premium P2 ou d’un abonnement de EMS E5 toouse Azure AD Privileged Identity Management.  tooget une version d’évaluation et démarrer à l’aide d’Azure AD Privileged Identity Management, lecture [prise en main Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

Si cette commande renvoie une ligne dans le SkuPartNumber est « AAD_PREMIUM_P2 » ou « EMSPREMIUM » et IsTrial est « True », cela indique que la période d’évaluation d’Azure AD Premium P2 est présent dans le locataire de hello.  Si l’état de l’abonnement hello n’est pas activé, et vous ne disposez pas d’un abonnement Azure AD Premium P2 ou EMS E5, vous devez acheter un abonnement de Azure AD Premium P2 ou d’un toocontinue d’abonnement EMS E5 à l’aide d’Azure AD Privileged Identity Management.

Azure AD Premium P2 est disponible via un [Microsoft Enterprise Agreement](https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx), hello [programme de licence en Volume Open](https://www.microsoft.com/en-us/licensing/licensing-programs/open-license.aspx)et hello [programme de fournisseurs de solutions de Cloud](https://partner.microsoft.com/en-US/cloud-solution-provider). Les abonnés Azure et Office 365 peuvent également acheter Azure AD Premium P2 en ligne.  Plus d’informations sur la tarification d’Azure AD Premium et comment tooorder en ligne, consultez [Azure Active Directory tarification](https://azure.microsoft.com/en-us/pricing/details/active-directory/).

## <a name="azure-ad-privileged-identity-management-is-not-available-in-tenant"></a>Azure AD Privileged Identity Management n’est pas disponible dans le locataire

Azure AD Privileged Identity Management ne sera plus disponible dans votre locataire si :
- Votre organisation utilisait la version préliminaire d’Azure AD Privileged Identity Management et n’a pas acheté d’abonnement Azure AD Premium P2 ou EMS E5.
- Votre organisation disposait d’une version d’évaluation d’Azure AD Premium P2 ou EMS E5 qui a expiré.
- Votre organisation a acheté un abonnement qui a expiré.

Lorsqu’un abonnement Azure AD Premium P2 ou EMS E5 arrive à expiration, ou qu’une organisation qui utilisait la version préliminaire d’Azure AD Privileged Identity Management n’achète pas d’abonnement Azure AD Premium P2 ou EMS E5 :

- Rôles de tooAzure AD affectations de rôle permanente ne sont pas affectés.
- Hello extension Azure AD Privileged Identity Management Bonjour portail Azure, ainsi que les applets de commande de l’API Graph hello et interfaces PowerShell d’Azure AD Privileged Identity Management, seront ne sont plus disponibles pour les utilisateurs des rôles de tooactivate privilégié, gérer un accès privilégié, ou effectuer des révisions d’accès des rôles privilégiés.
- Éligibles attributions de rôles Azure AD sont supprimées, car les utilisateurs ne seront plus en mesure de tooactivate privilégié rôles.
- Les vérifications d’accès en cours de rôles sont terminées, et les paramètres de configuration d’Azure AD Privileged Identity Management sont supprimés.
- Azure AD Privileged Identity Management n’envoie plus de messages électroniques sur les modifications apportées aux affectations de rôle.

## <a name="next-steps"></a>Étapes suivantes

- [Prise en main d’Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md)
- [Rôles dans Azure AD Privileged Identity Management](../active-directory-privileged-identity-management-roles.md)
