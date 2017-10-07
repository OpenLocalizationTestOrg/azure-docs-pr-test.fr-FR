---
title: 'Azure AD Connect Sync : Activer la Corbeille AD | Microsoft Docs'
description: "Cette rubrique recommande l’utilisation de hello de fonctionnalité de corbeille Active Directory avec Azure AD Connect."
services: active-directory
keywords: Corbeille AD, suppression accidentelle, ancre source
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: afec4207-74f7-4cdd-b13a-574af5223a90
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2bb4827d677ccecfd8d2861f2a2fcf73b8cc2d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-enable-ad-recycle-bin"></a>Azure AD Connect Sync : Activer la Corbeille AD
Il est recommandé d’activer la fonctionnalité de Corbeille hello AD pour vos annuaires Active Directory local, qui sont synchronisé tooAzure AD. 

Si vous avez supprimé par inadvertance un site local objet utilisateur AD et restauration à l’aide de la fonctionnalité de hello, Azure AD restaure objet utilisateur Azure AD correspondant de hello.  Pour plus d’informations sur la fonctionnalité de Corbeille hello AD, consultez tooarticle [vue d’ensemble du scénario de restauration des objets Active Directory supprimés](https://technet.microsoft.com/library/dd379542.aspx).

## <a name="benefits-of-enabling-hello-ad-recycle-bin"></a>Avantages de l’activation de hello AD la Corbeille
Cette fonctionnalité permet à la restauration des objets utilisateur Azure AD de manière hello suivante :

* Si vous avez accidentellement supprimé localement l’objet utilisateur Active Directory, objet utilisateur Azure AD correspondant de hello est supprimé dans hello prochain cycle de synchronisation. Par défaut, Azure AD conserve un objet d’utilisateur Azure AD hello supprimé supprimé l’état pendant 30 jours.

* Si vous avez localement fonctionnalité Corbeille Active Directory est activée, vous pouvez restaurer hello supprimé localement objet utilisateur AD sans modifier sa valeur d’ancre Source. Lorsque hello récupérées localement synchronisation de l’objet utilisateur AD tooAzure AD, Azure AD permet de restaurer hello correspondant supprimé objet utilisateur Azure AD. Pour plus d’informations sur l’attribut d’ancrage de la Source, consultez tooarticle [Azure AD Connect : concepts de conception](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#sourceanchor).

* Si vous n’avez pas local AD recycler fonctionnalité Corbeille activée, vous pouvez toocreate requis AD utilisateur tooreplace hello supprimés d’objet. Si Service de synchronisation Azure AD Connect est configuré toouse généré par le système attribut AD (par exemple, ObjectGuid) pour l’attribut d’ancre Source hello, hello objet d’utilisateur Active Directory qui vient d’être créé ne sera pas avoir hello même valeur d’ancre Source comme hello supprimé l’objet utilisateur AD. Lorsque hello nouvellement créé l’objet utilisateur Active Directory est synchronisé tooAzure AD, Azure AD crée un nouvel objet utilisateur d’Azure AD au lieu de restaurer l’objet d’utilisateur Azure AD hello supprimé.

> [!NOTE]
> Par défaut, AD Azure conserve les objets d’utilisateur Azure AD dans un état supprimé temporairement pendant 30 jours avant suppression définitive. Toutefois, les administrateurs peuvent accélérer la suppression de ces objets hello. Une fois que les objets hello sont définitivement supprimés, ils ne peuvent plus être restaurées, même si locaux Corbeille Active Directory est activée.



## <a name="next-steps"></a>Étapes suivantes
**Rubriques de présentation**

* [Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation](active-directory-aadconnectsync-whatis.md)

* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)
