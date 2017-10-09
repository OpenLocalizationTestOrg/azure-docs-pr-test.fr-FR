---
title: "aaaUpgrade à partir de DirSync et Azure AD Sync | Documents Microsoft"
description: "Décrit comment tooupgrade à partir de DirSync et Azure AD Sync tooAzure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: bd68fb88-110b-4d76-978a-233e15590803
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d465b137fb54f0c6e28ccf73429c4bd3aafd8698
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-windows-azure-active-directory-sync-and-azure-active-directory-sync"></a>Mettre à niveau Microsoft Azure Active Directory Sync et Azure Active Directory Sync
Azure AD Connect est hello meilleure manière tooconnect votre annuaire local avec Azure AD et Office 365. Il s’agit d’un tooAzure de tooupgrade beaucoup de temps AD Connect à partir de Windows Azure Active Directory Sync (DirSync) ou Azure AD Sync que ces outils sont déconseillées maintenant et fin de la prise en charge sur le 13 avril 2017.

Hello deux identité outils de synchronisation qui sont déconseillées ont été proposées pour les clients de forêt unique (DirSync) et pour plusieurs forêts et d’autres clients avancés (Azure AD Sync). Ces outils plus anciens ont été remplacés par une solution unique qui est disponible pour tous les scénarios : Azure AD Connect. Cette solution offre de nouvelles fonctionnalités, des améliorations de fonctionnalités et la prise en charge de nouveaux scénarios. toobe toocontinue en mesure de toosynchronize de votre tooAzure de données d’identité locale AD et Office 365, nous recommandons que vous mettez à niveau tooAzure AD Connect.

Hello dernière version de synchronisation d’annuaire a été publiée en juillet 2014 et la dernière version de hello d’Azure AD Sync a été publiée en mai 2015.

## <a name="what-is-azure-ad-connect"></a>Qu’est-ce qu’Azure AD Connect ?
Azure AD Connect est hello successeur tooDirSync et Azure AD Sync. Il combine tous les scénarios pris en charge par les deux autres. Pour en savoir plus, consultez [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

## <a name="deprecation-schedule"></a>Planification de la désapprobation
| Date | Commentaire |
| --- | --- |
| 13 avril 2016 |Microsoft Azure Active Directory Sync (« DirSync ») et Azure Active Directory Sync (« Azure AD Sync ») sont annoncés comme déconseillés. |
| 13 avril 2017 |Fin de la prise en charge. Les clients ne seront plus en mesure de tooopen un cas de prise en charge sans mettre à niveau tooAzure AD se connecter en premier. |
|31 décembre 2017|Azure AD n’acceptera plus de communications provenant de Windows Azure Active Directory Sync (« DirSync ») et de Microsoft Azure Active Directory Sync (« Azure AD Sync »).

## <a name="how-tootransition-tooazure-ad-connect"></a>Comment tootransition tooAzure AD Connect
Si vous exécutez DirSync, vous disposez de deux méthodes de mise à niveau : mise à niveau sur place et déploiement parallèle. Une mise à niveau sur place est recommandée pour la plupart des clients et si vous avez un système d’exploitation récent avec moins de 50 000 objets. Dans d’autres cas, il est recommandé de toodo un déploiement parallèle où votre configuration DirSync est déplacé tooa nouveau serveur exécutant Azure AD Connect.

Si vous utilisez Azure AD Sync, une mise à niveau sur place est recommandée. Si vous le souhaitez, il est possible de tooinstall un nouveau serveur Azure AD Connect en parallèle et effectuer un basculement de migration à partir de votre tooAzure de serveur Azure AD Sync AD Connect.

| Solution | Scénario |
| --- | --- |
| [Mise à niveau à partir de DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>Si vous disposez d’un serveur DirSync existant déjà en cours d’exécution.</li> |
| [Mise à niveau à partir d’Azure AD Sync](active-directory-aadconnect-upgrade-previous-version.md) |<li>Si vous effectuez la mise à niveau à partir d’Azure AD Sync.</li> |

Si vous souhaitez toosee comment toodo un emplacement de mise à niveau à partir de la synchronisation d’annuaire tooAzure AD Connect, puis consultez cette vidéo de Channel 9 :

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Azure-Active-Directory-Connect-in-place-upgrade-from-legacy-tools/player]
>
>

## <a name="faq"></a>Forum Aux Questions
**Q : j’ai reçu une notification par courrier électronique à partir de hello équipe Azure et/ou d’un message à partir du centre de messages hello Office 365, mais j’utilise la connexion.**  
notification de Hello a été envoyée également toocustomers à l’aide d’Azure AD Connect avec un numéro de version 1.0. \*.0 (à l’aide d’une version pre-1.1). Microsoft vous recommande de clients toostay actuel avec Azure AD Connect libère. Hello [mise à niveau automatique](active-directory-aadconnect-feature-automatic-upgrade.md) fonctionnalité introduite dans la version 1.1, il est facile tooalways une version récente d’Azure AD Connect installée.

**Q : DirSync/Azure AD Sync vont-ils cesser de fonctionner le 13 avril 2017 ?**  
DirSync/Azure AD Sync continue toowork sur avril 2017 de 13.  Cependant, Azure AD n’acceptera plus les communications provenant de DirSync/Azure AD Sync à partir du 31 décembre 2017.

**Q: Quelles versions de DirSync puis-je mettre à niveau ?**  
Il est pris en charge tooupgrade à partir de n’importe quelle version de synchronisation d’annuaire en cours d’utilisation.

**Q : que se passe-t-il sur hello connecteur Azure AD pour FIM/MIM ?**  
Hello connecteur Azure AD pour FIM/MIM a **pas** été annoncées comme déconseillées. Il est dans l’état **feature freeze**; aucune nouvelle fonctionnalité n’est ajoutée et il ne reçoit aucune résolution de bogue. Microsoft vous recommande de clients qui utilisent le toomove tooplan à partir de celui-ci tooAzure AD Connect. Il est fortement recommandé de toonot démarrer tous les nouveaux déploiements à l’utiliser. Ce connecteur est annoncé déconseillée Bonjour futures.

## <a name="additional-resources"></a>Ressources supplémentaires
* [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md)
