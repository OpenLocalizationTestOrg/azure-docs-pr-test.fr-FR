---
title: "Dépannage : « Active Directory » est manquant ou non disponible | Documents Microsoft"
description: "Le toodo lors de l’élément de menu Active Directory n’apparaît pas dans hello portail de gestion Azure."
services: active-directory
documentationcenter: na
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 3383020d-6397-43ea-b7aa-c6a9d6a1e3df
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.openlocfilehash: d7355a4e39141f0b09272dc5615c309b23c8c70f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-active-directory-item-is-missing-or-not-available"></a>Dépannage : l’élément « Active Directory » est manquant ou non disponible
De nombreuses instructions hello pour l’utilisation de services et les fonctionnalités d’Azure Active Directory commencent par « accédez toohello portail de gestion Azure et cliquez sur **Active Directory**. » Mais que faire si hello Active Directory extension ou élément de menu ne s’affiche pas ou si elle est marquée **non disponible**? Cette rubrique est conçue toohelp. Il décrit dans quelles conditions de hello **Active Directory** n’apparaît pas ou n’est pas disponible et explique comment tooproceed.

## <a name="active-directory-is-missing"></a>Active Directory est manquant
En règle générale, une **Active Directory** élément apparaît dans le menu de navigation gauche hello. instructions de Hello dans les procédures d’Azure Active Directory supposent que cet élément est visible.

![Capture d’écran : Active Directory dans Azure](./media/active-directory-troubleshooting/typical-view.png)

élément d’Active Directory Hello s’affiche dans le menu de navigation gauche hello lorsqu’une de hello conditions suivantes est vraie. Sinon, l’élément de hello n’apparaît pas.

* l’utilisateur actuel Hello connecté avec un compte Microsoft (anciennement un identifiant Windows Live ID).
  
    OU
* Hello locataire Azure possède un répertoire et compte de hello actuel est un administrateur d’annuaire.
  
    OU
* Hello locataire Azure possède au moins un espace de noms Azure AD Access Control (ACS). Pour plus d’informations, consultez la page [À propos des noms d’espaces de contrôle d’accès](https://msdn.microsoft.com/library/azure/gg185908.aspx).
  
    OU
* Hello locataire Azure possède au moins un fournisseur multi-Factor Authentication. Pour plus d’informations, consultez la rubrique [Administration des fournisseurs Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md).

toocreate un espace de noms de contrôle d’accès ou un fournisseur multi-Factor Authentication, cliquez sur **+ nouveau** > **des Services d’application** > **Active Directory**.

répertoire de tooa tooget droits d’administration, ont un administrateur attribuer à un administrateur tooyour compte membre du rôle. Pour plus de détails, consultez [Attribution de rôles d’administrateur](active-directory-assign-admin-roles.md)

## <a name="active-directory-is-not-available"></a>Active Directory n’est pas disponible
Lorsque vous cliquez sur **+ New** > **App Services**, un élément **Active Directory** s’affiche. Plus précisément, élément d’Active Directory hello s’affiche lorsqu’une des fonctionnalités d’Active Directory hello, tels que le répertoire, le contrôle d’accès ou fournisseur d’authentification multifacteur est disponible toohello l’utilisateur actuel.

Toutefois, pendant le chargement de page de hello, élément de hello est estompé et est marqué comme **non disponible**. Il s’agit d’un état temporaire. Si vous attendez quelques secondes, l’élément de hello devienne disponible. Si le délai de hello se prolonge, l’actualisation page web de hello résout souvent problème de hello.

![Capture d’écran : Active Directory n’est pas disponible](./media/active-directory-troubleshooting/not-available.png)

