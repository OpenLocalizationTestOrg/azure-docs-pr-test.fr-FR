---
title: "vue d’ensemble d’aaaConceptual des noms de domaines personnalisés dans Azure Active Directory | Documents Microsoft"
description: "Explique l’infrastructure conceptuelle de hello pour l’utilisation de noms de domaines personnalisés dans Azure Active directory, y compris la fédération pour l’authentification unique"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: fd0c5def-0da2-43af-81bc-76f4cfe86afd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 0a3454ae6b733a8a13a71925df3cc664063f388e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="conceptual-overview-of-custom-domain-names-in-azure-active-directory"></a>Vue d’ensemble conceptuelle des noms de domaine personnalisés dans Azure Active Directory
Un nom de domaine peut être un identificateur important pour de nombreuses ressources de répertoire, lorsqu’il est compris dans :

* Un nom d’utilisateur ou une adresse e-mail d’un utilisateur
* adresse Hello pour un groupe
* URI ID d’application Hello pour une application

Une ressource dans Azure Active Directory (Azure AD) peut inclure un nom de domaine qui est a déjà été vérifié toobe détenus par le répertoire de hello qui contient les ressources hello. Seul un administrateur général peut effectuer des tâches de gestion de domaine dans Azure AD.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. Pour comment toomanage vos noms de domaine dans le centre d’administration hello Azure AD, consultez [la gestion des noms de domaines personnalisés dans Azure Active Directory](active-directory-domains-manage-azure-portal.md).

Les noms de domaine dans Azure AD sont globalement uniques. Un nom de domaine personnalisé ne peut être utilisé que par un seul locataire Azure AD à la fois. Si un répertoire Azure AD a vérifié un nom de domaine, aucun autre répertoire Azure AD ne peut vérifier ou utiliser ce même nom de domaine.

## <a name="initial-and-custom-domain-names"></a>Noms de domaine initial et personnalisé
Chaque nom de domaine dans Azure AD est un nom de domaine initial ou un nom de domaine personnalisé.

Chaque Azure AD est fourni avec un nom de domaine initial dans hello formulaire contoso.onmicrosoft.com. Ce nom de domaine de niveau tiers, dans cet exemple, « contoso.onmicrosoft.com », a été établi lors de l’annuaire de hello a été créé, en général par l’administrateur hello qui a créé le répertoire de hello. nom de domaine initial Hello pour un répertoire ne peut pas être modifiée ou supprimée. nom de domaine initial Hello, bien qu’entièrement fonctionnelles, vise principalement les toobe utilisé comme un mécanisme d’amorçage jusqu'à ce que le nom de domaine personnalisé est vérifié.

Dans la plupart des environnements de production, un répertoire contient au moins un domaine personnalisé vérifié, par exemple, « contoso.com », et il s’agit de ce domaine personnalisé est visible tooend utilisateurs. Un nom de domaine personnalisé est un nom de domaine qui est la propriété et qui est utilisé par cette organisation, par exemple, « contoso.com », pour des utilisations comme l’hébergement de son site web. Ce nom de domaine est tooemployees familier, car il fait partie du nom d’utilisateur hello qu’ils utilisent toosign dans un réseau d’entreprise toohello ou toosend et récupérer le courrier électronique.

Avant de pouvoir être utilisé par Azure AD, le nom de domaine personnalisé hello doit être ajouté tooyour répertoire et vérifié.

## <a name="verified-and-unverified-domain-names"></a>Noms de domaine vérifiés et non vérifiés
nom de domaine initial Hello pour un répertoire est implicitement évaluée comme vérifié par Azure AD. Lorsqu’un administrateur ajoute un tooan de nom de domaine personnalisé Azure AD, il est initialement dans un état non vérifié. Azure AD ne permet pas de n’importe quel toouse de ressources Active un nom de domaine non vérifié. Cela garantit qu’un seul répertoire peut utiliser un nom de domaine, et qu’organisation de hello utilise le nom de domaine hello réellement propriétaire de ce nom de domaine.

Azure AD vérifie la propriété de nom de domaine en recherchant une entrée particulière dans le fichier de zone hello domaine nom du service (DNS) pour le nom de domaine hello. tooverify la propriété d’un nom de domaine, un administrateur obtient hello DNS entrée à partir d’Azure AD que Azure AD recherchera et ajoute ce fichier de zone DNS toohello entrée pour le nom de domaine hello. fichier de zone DNS Hello est géré par le bureau d’enregistrement du nom de domaine hello pour ce domaine. Hello étapes tooverify est un domaine sont affichés dans l’article hello pour [Ajout d’un répertoire de tooyour Azure AD du domaine personnalisé](active-directory-add-domain.md).

Ajout d’un fichier de zone toohello entrée DNS pour le nom de domaine hello n’affecte pas les autres services de domaine telles que l’adresse de messagerie ou d’hébergement web.

## <a name="federated-and-managed-domain-names"></a>Noms de domaines fédérés et gérés
Un nom de domaine personnalisé dans Azure AD peuvent être configuré toogive utilisateurs une expérience entre votre Active Directory local et le Azure AD de connexion fédérée. Configuration d’un domaine pour la fédération requiert des mises à jour les ressources tooprivileged dans Azure AD et également tooyour Windows Server Active Directory. La configuration d’un domaine fédéré doit être effectuée à partir d’Azure AD Connect ou à l’aide de PowerShell. Fédérer un domaine personnalisé ne peut pas être lancé à partir de hello portail Azure classic. [Regardez cette vidéo toolearn sur la configuration AD FS pour l’authentification utilisateur avec Azure AD Connect](http://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Configuring-AD-FS-for-user-sign-in-with-Azure-AD-Connect).

Les domaines qui ne sont pas fédérés sont parfois appelés domaines gérés. domaine initial de Hello pour un annuaire Azure AD est implicitement évalué comme un domaine géré.

## <a name="primary-domain-names"></a>Noms de domaines principaux
nom de domaine principal pour un répertoire Hello est nom de domaine hello est présélectionné en tant que valeur par défaut de hello pour la partie de hello 'domaine' hello nom d’utilisateur, lorsqu’un administrateur crée un nouvel utilisateur Bonjour [portail Azure](https://portal.azure.com/), ou un autre portail tels que le portail d’administration hello Office 365 ou portail de Microsoft Intune hello. Un répertoire ne peut avoir qu’un seul nom de domaine principal. Un administrateur peut modifier toobe de nom de domaine principal hello n’importe quel domaine personnalisé vérifié qui n’est pas fédéré ou toohello du domaine initial.

## <a name="domain-names-in-azure-ad-and-other-microsoft-online-services"></a>Noms de domaine dans Azure AD et dans les autres services Microsoft Online Services
Un nom de domaine doit être vérifié dans Azure AD avant de pouvoir être utilisé par un autre service Microsoft Online Service, comme Exchange Online, SharePoint Online et Intune. Ces autres services requièrent généralement une tooadd administrateur une ou plusieurs entrées DNS qui sont notamment toohello service.

Une application web Azure utilise son propre mécanisme tooverify la propriété d’un domaine. Pour une utilisation avec Azure AD, un domaine doit être vérifié, même s’il a précédemment été vérifié pour une utilisation par une application web Azure dans un abonnement qui s’appuie sur Azure AD. Une application web Azure permettre utiliser un nom de domaine qui a été vérifié dans un répertoire différent de celui de répertoire hello qui sécurise hello web app.

## <a name="managing-domain-names"></a>Gestion des noms de domaine
Tâches de gestion de domaine peuvent être effectuées à partir de hello portail Azure classic et à partir de PowerShell. De nombreuses tâches peuvent être effectuées à l’aide des API d’Azure AD Graph hello.

* [Ajout et vérification d’un nom de domaine personnalisé](active-directory-add-domain.md)
* [La gestion des domaines Bonjour portail Azure classic](active-directory-add-manage-domain-names.md)
* [À l’aide de noms de domaine toomanage PowerShell dans Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [À l’aide de noms de domaine toomanage hello API Azure AD Graph dans Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

