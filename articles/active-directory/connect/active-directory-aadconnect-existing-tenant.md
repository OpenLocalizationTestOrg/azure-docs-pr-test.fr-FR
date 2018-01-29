---
title: "Azure AD Connect : lorsque vous avez déjà Azure AD | Microsoft Docs"
description: "Cette rubrique décrit comment utiliser Connect lorsque vous avez un client Azure AD existant."
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: fa264487c68ea5403300d9b5b9978934a639a2a4
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/18/2018
---
# <a name="azure-ad-connect-when-you-have-an-existent-tenant"></a>Azure AD Connect : lorsque vous avez un client existant
La plupart des rubriques sur l’utilisation d’Azure AD Connect suppose que vous démarrez avec un nouveau client Azure AD qui ne contient aucun utilisateur ni autres objets. Mais si vous avez démarré avec un client Azure AD, auquel vous avez ajouté des utilisateurs et d’autres objets, et que vous souhaitez désormais utiliser Connect, alors cette rubrique est faite pour vous.

## <a name="the-basics"></a>Concepts de base
Un objet dans Azure AD est soit contrôlé dans le cloud (Azure AD), soit local. Pour un objet unique, vous ne pouvez pas gérer certains attributs en local et d’autres attributs dans Azure AD. Chaque objet dispose d’un indicateur qui indique où l’objet est géré.

Vous pouvez gérer certains utilisateurs en local et d’autres dans le cloud. Un scénario courant pour cette configuration est une organisation qui regroupe des comptables et des commerciaux. Les comptables ont un compte AD local, mais les commerciaux n’en ont pas. Ils disposent d’un compte dans Azure AD. Vous devez alors gérer certains utilisateurs en local et d’autres dans Azure AD.

Si vous avez commencé à gérer des utilisateurs dans Azure AD qui se trouvent également dans un répertoire AD local et que vous souhaitez ultérieurement utiliser Connect, il existe des considérations supplémentaires que vous devez prendre en compte.

## <a name="sync-with-existing-users-in-azure-ad"></a>Synchroniser avec les utilisateurs existants dans Azure AD
Lorsque vous installez Azure AD Connect et démarrez la synchronisation, le service de synchronisation Azure AD (dans Azure AD) effectue une vérification de chaque nouvel objet et essaie de trouver un objet existant correspondant. Il existe trois attributs utilisés pour ce processus : **userPrincipalName**, **proxyAddresses** et **sourceAnchor**/**immutableID**. Une correspondance avec **userPrincipalName** et avec **proxyAddresses** est appelée une **correspondance souple**. Une correspondance avec **sourceAnchor** est appelée une **correspondance exacte**. Pour l’attribut **proxyAddresses**, seule la valeur avec **SMTP :**, c’est-à-dire l’adresse e-mail principale, est utilisée pour l’évaluation.

La correspondance est évaluée uniquement pour les nouveaux objets provenant de Connect. Si vous modifiez un objet existant afin qu’il corresponde à l’un de ces attributs, une erreur s’affiche à la place.

Si AD Azure détecte un objet dans lequel les valeurs d’attribut sont les mêmes pour un objet provenant de Connect et qui est déjà présent dans Azure AD, alors l’objet dans Azure AD est pris en charge par Connect. L’objet précédemment géré dans le cloud est indiqué comme étant géré en local. Tous les attributs dans Azure AD avec une valeur dans le répertoire AD local sont remplacés par la valeur locale. L’exception est lorsqu’un attribut a une valeur **NULL** locale. Dans ce cas, la valeur dans Azure AD est conservée, mais vous pouvez toujours la modifier uniquement en local.

> [!WARNING]
> Étant donné que tous les attributs dans Azure AD vont être remplacés par la valeur locale, assurez-vous que vous disposez de bonnes données locales. Par exemple, si vous avez uniquement une adresse e-mail gérée dans Office 365 et que vous ne l’avez pas conservée à jour dans AD DS en local, alors vous perdrez toutes les valeurs dans Azure AD/Office 365 qui ne figurent pas dans AD DS.

> [!IMPORTANT]
> Si vous utilisez la synchronisation de mot de passe, qui est toujours utilisée par la configuration rapide, alors le mot de passe dans Azure AD est remplacé par le mot de passe dans le répertoire AD local. Si vos utilisateurs sont habitués à gérer des mots de passe différents, vous devez alors les informer qu’ils doivent utiliser le mot de passe local une fois Connect installé.

La section précédente et l’avertissement qu’elle contient doivent être pris en compte lors de la planification. Si vous avez effectué de nombreuses modifications dans Azure AD qui ne sont pas reflétées dans AD DS en local, vous devez alors planifier comment renseigner AD DS avec les valeurs mises à jour avant de synchroniser vos objets avec Azure AD Connect.

Si vous avez exécuté la correspondance de vos objets avec une correspondance souple, l’attribut **sourceAnchor** est ajouté à l’objet dans Azure AD afin qu’une correspondance exacte soit utilisée ultérieurement.

### <a name="hard-match-vs-soft-match"></a>Correspondance exacte et correspondance souple
Pour une nouvelle installation de Connect, il n’existe aucune différence pratique entre une correspondance souple et une correspondance exacte. La différence réside dans une situation de récupération d’urgence. Si votre serveur avec Azure AD Connect a connu une défaillance, vous pouvez réinstaller une nouvelle instance sans perdre de données. Un objet avec un attribut sourceAnchor est envoyé à Connect lors de l’installation initiale. La correspondance peut ensuite être évaluée par le client (Azure AD Connect), ce qui est beaucoup plus rapide que de faire la même chose dans Azure AD. Une correspondance exacte est évaluée à la fois par Connect et par Azure AD. Une correspondance souple n’est évaluée que par Azure AD.

### <a name="other-objects-than-users"></a>Objets autres que des utilisateurs
Pour les groupes et les contacts activés pour le courrier, vous pouvez établir une correspondance souple en fonction de proxyAddresses. La correspondance exacte n’est pas applicable dans la mesure où vous pouvez seulement mettre à jour sourceAnchor/immutableID (à l’aide de PowerShell) sur les utilisateurs uniquement. Pour les groupes qui ne sont pas activés pour le courrier, il n’existe actuellement aucune prise en charge pour la correspondance souple ou la correspondance exacte.

## <a name="create-a-new-on-premises-active-directory-from-data-in-azure-ad"></a>Créer un nouveau répertoire Active Directory local à partir des données dans Azure AD
Certains clients démarrent avec une solution cloud uniquement avec Azure AD et ils ne disposent pas d’un répertoire AD local. Ensuite, ils souhaitent consommer des ressources locales et créer un répertoire AD local basé sur les données d’Azure AD. Azure AD Connect ne peut pas vous aider dans ce scénario. Il ne crée pas d’utilisateurs locaux et il ne peut pas définir le mot de passe local pour qu’il soit le même que dans Azure AD.

Si la seule raison pour laquelle vous souhaitez ajouter un répertoire AD local est pour la prise en charge d’applications métier, vous devrez peut-être envisager d’utiliser les [services de domaine Azure AD](../../active-directory-domain-services/index.md) à la place.

## <a name="next-steps"></a>étapes suivantes
En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
