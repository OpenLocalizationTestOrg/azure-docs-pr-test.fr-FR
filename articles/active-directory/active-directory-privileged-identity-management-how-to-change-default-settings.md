---
title: "paramètres de l’activation du rôle aaaHow toomanage | Documents Microsoft"
description: "Découvrez comment toochange hello les paramètres par défaut pour les identités privilégiées avec hello extension d’Azure Active Directory Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a>Comment les paramètres de l’activation de rôle toomanage dans Azure AD Privileged Identity Management
Un administrateur de rôle privilégié peut personnaliser Azure AD Privileged Identity Management (PIM) dans leur organisation, notamment en modifiant l’expérience hello pour un utilisateur qui est d’activer une attribution de rôle éligible.

## <a name="manage-hello-role-activation-settings"></a>Gérer les paramètres de l’activation de rôle hello
1. Accédez toohello [portail Azure](https://portal.azure.com) et sélectionnez hello **Azure AD Privileged Identity Management** application à partir du tableau de bord hello.
2. Sélectionnez **Gérer les rôles privilégiés** > **Paramètres** > **Rôles privilégiés**.
3. Choisissez le rôle de hello dont les paramètres souhaités toomanage.

Sur la page de paramètres hello pour chaque rôle, il existe un nombre de paramètres que vous pouvez configurer. Ces paramètres affectent uniquement les utilisateurs qui sont des administrateurs éligibles et non des administrateurs permanents.

**Les activations**: hello durée, en heures, pendant laquelle un rôle reste actif avant son expiration. Cette durée peut être comprise entre 1 et 72 heures.

**Notifications**: vous pouvez choisir ou non système de hello envoie tooadmins e-mails confirmant qu’ils ont activé un rôle. Cette option peut être utile pour détecter les activations non autorisées ou illégitimes.

**Ticket d’incident/demande**: vous pouvez choisir ou non toorequire administrateurs éligibles tooinclude un ticket de numéro de leur activation de leur rôle. Cela peut être utile lorsque vous effectuez des audits d’accès à un rôle.

**L’authentification multifacteur**: vous pouvez choisir ou non toorequire utilisateurs tooverify leur identité avec l’authentification Multifacteur, avant de pouvoir activer leurs rôles. Ils ont uniquement tooverify ce qu’une seule fois par session, pas chaque fois qu’ils activer un rôle. Il existe deux tookeep de conseils à l’esprit lorsque vous activez l’authentification Multifacteur :

* Les utilisateurs qui disposent de comptes Microsoft pour leurs adresses de messagerie (généralement @outlook.com, mais pas toujours) ne peut pas inscrire pour Azure MFA. Si vous souhaitez toousers de rôles tooassign avec des comptes Microsoft, vous devez les rendre administrateurs permanents ou désactiver l’authentification Multifacteur pour ce rôle.
* Vous ne pouvez pas désactiver l’authentification multifacteur pour les rôles à privilèges élevés pour Azure AD et Office 365. Il s’agit d’une fonctionnalité de sécurité car ces rôles doivent être soigneusement protégés :  
  
  * Administrateur d’application
  * Administrateur du serveur proxy d’application
  * Administrateur de facturation  
  * Administrateur de conformité  
  * Administrateur de services CRM
  * Approbateur d’accès au référentiel sécurisé client
  * Enregistreur de répertoire  
  * Administrateur Exchange  
  * Administrateur général
  * Administrateur de services Intune
  * Administrateur de boîte aux lettres  
  * Prise en charge de niveau 1 de partenaire  
  * Prise en charge de niveau 2 de partenaire  
  * Administrateur de rôle privilégié   
  * Administrateur de sécurité  
  * Administrateur SharePoint  
  * Administrateur Skype Entreprise  
  * Administrateur de compte d’utilisateur  

Pour plus d’informations sur l’utilisation de l’authentification Multifacteur avec PIM consultez [comment tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Étapes suivantes
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

