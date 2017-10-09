---
title: "Azure AD Connect : fonctionnalités de la version préliminaire | Microsoft Docs"
description: "Cette rubrique décrit en détail les fonctionnalités disponibles en version préliminaire dans Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: bcfc710861b19d8f86f094ced0d1c691e0911f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="more-details-about-features-in-preview"></a>Plus de détails sur les fonctionnalités de la version préliminaire
Cette rubrique décrit comment toouse fonctionnalités actuellement en version préliminaire.

## <a name="group-writeback"></a>Écriture différée de groupe
option Hello pour l’écriture différée de groupe dans des fonctionnalités facultatives vous permet de toowriteback **les groupes Office 365** forêt tooa avec Exchange est installé. Il s’agit d’un groupe qui est toujours masterisé dans le cloud de hello. Si vous avez Exchange sur site, puis vous pouvez écrire dans ces groupes tooon locaux pour les utilisateurs disposant d’une boîte aux lettres Exchange de local peuvent envoyer et recevoir des courriers électroniques à partir de ces groupes.

Plus d’informations sur les groupes Office 365 et comment toouse les trouverez [ici](http://aka.ms/O365g).

Un groupe Office 365 est représenté comme un groupe de distribution dans les versions locales d’AD DS. Votre Exchange server sur site doit être sur Exchange 2013 mise à jour cumulative 8 (publiée en mars 2015) ou Exchange 2016 toorecognize ce nouveau type de groupe.

**Notes de version préliminaire hello**

* attribut de carnet d’adresses Hello n’est actuellement pas remplie dans l’aperçu de hello. Sans cet attribut, groupe de hello n’est pas visible dans la liste d’adresses globale de hello. Hello toopopulate de façon plus simple cet attribut est l’applet de commande PowerShell Exchange toouse hello `update-recipient`.
* Seules les forêts avec schéma de Exchange hello sont des cibles valides pour les groupes. Si aucun Exchange a été détecté, l’écriture différée de groupe n’est pas possible tooenable.
* Seuls les déploiements d’entreprise basés sur une seule forêt Exchange sont actuellement pris en charge. Si vous avez plusieurs Exchange organisation sur site, vous devez une solution GALSync établit un local pour tooappear de ces groupes dans vos autres forêts.
* fonctionnalité d’écriture différée de groupe de Hello ne gère pas les groupes de sécurité ou des groupes de distribution.

> [!NOTE]
> Un tooAzure abonnement Premium d’Active Directory est requis pour l’écriture différée de groupe.
> 
>

## <a name="user-writeback"></a>Écriture différée de l’utilisateur
> [!IMPORTANT]
> fonctionnalité d’aperçu de l’écriture différée d’utilisateur Hello a été supprimée dans tooAzure de mise à jour d’août 2015 hello AD Connect. Si vous l'avez activée, vous devez désactiver cette fonctionnalité.
>
>

## <a name="next-steps"></a>Étapes suivantes
Poursuivez votre [installation personnalisée d’Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
