---
title: "Azure AD Connect : lorsque vous avez déjà Azure AD | Microsoft Docs"
description: "Cette rubrique décrit comment toouse connecter lorsque vous avez un locataire Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f7b166e9e85c1f03330e8e0074d4afa4036738c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-when-you-have-an-existent-tenant"></a>Azure AD Connect : lorsque vous avez un client existant
La plupart des rubriques hello pour comment toouse Azure AD Connect suppose que vous démarrez avec un nouveau Azure client AD et qu’il n’y a aucun utilisateur ou autres objets. Mais si vous avez démarré avec un locataire Azure AD, rempli avec les utilisateurs et d’autres objets, il et voulez présent toouse se connecter, puis cette rubrique est pour vous.

## <a name="hello-basics"></a>principes de base Hello
Un objet dans Azure AD est masterisé soit dans le cloud hello (Azure AD) ou localement. Pour un objet unique, vous ne pouvez pas gérer certains attributs en local et d’autres attributs dans Azure AD. Chaque objet a un indicateur qui indique où l’objet de hello est géré.

Vous pouvez gérer des utilisateurs locaux et autres dans le cloud de hello. Un scénario courant pour cette configuration est une organisation qui regroupe des comptables et des commerciaux. traitements comptables Hello ont un site local compte Active Directory, mais les threads de travail ventes hello ne le faites pas, ils disposent d’un compte dans Azure AD. Vous devez alors gérer certains utilisateurs en local et d’autres dans Azure AD.

Si vous avez démarré toomanage utilisateurs dans Azure AD qui sont également dans AD local et décidez toouse se connecter, puis il existe des problèmes supplémentaires, que vous devez tooconsider.

## <a name="sync-with-existing-users-in-azure-ad"></a>Synchroniser avec les utilisateurs existants dans Azure AD
Lorsque vous installez Azure AD Connect et démarrer la synchronisation, hello service de synchronisation Azure AD (dans Azure AD) effectue une vérification pour chaque nouvel objet et recommencez toofind un toomatch objet existant. Il existe trois attributs utilisés pour ce processus : **userPrincipalName**, **proxyAddresses** et **sourceAnchor**/**immutableID**. Une correspondance avec **userPrincipalName** et avec **proxyAddresses** est appelée une **correspondance souple**. Une correspondance avec **sourceAnchor** est appelée une **correspondance exacte**. Pourquoi **proxyAddresses** uniquement hello valeur avec attribut **SMTP :**, qui est l’adresse de messagerie principale hello, qui est utilisé pour l’évaluation de hello.

correspondance de Hello est évaluée uniquement pour les nouveaux objets provenant de se connecter. Si vous modifiez un objet existant afin qu’il corresponde à l’un de ces attributs, une erreur s’affiche à la place.

Si AD Azure détecte un objet dans lequel les valeurs d’attribut hello sont hello même pour un objet provenant de se connecter et qui il est déjà présent dans Azure AD, puis hello objet dans Azure AD est prise en charge de la connexion. Hello précédemment objet cloud géré est marqué comme géré sur site. Tous les attributs dans Azure AD avec une valeur locale Active Directory sont remplacées par valeur locale de hello. exception de Hello est lorsqu’un attribut a un **NULL** valeur locale. Dans ce cas, valeur hello dans Azure AD reste, mais vous pouvez toujours uniquement la modifier toosomething local autre.

> [!WARNING]
> Étant donné que tous les attributs dans Azure AD apprêtez toobe remplacée par la valeur locale de hello, assurez-vous que vous disposez des données localement. Par exemple, si vous avez uniquement une adresse e-mail gérée dans Office 365 et que vous ne l’avez pas conservée à jour dans AD DS en local, alors vous perdrez toutes les valeurs dans Azure AD/Office 365 qui ne figurent pas dans AD DS.

> [!IMPORTANT]
> Si vous utilisez la synchronisation de mot de passe, qui est toujours utilisée par les paramètres express, puis un mot de passe hello dans Azure AD est remplacé par un mot de passe hello locaux Active Directory. Si vos utilisateurs sont utilisés toomanage différent des mots de passe, vous devez tooinform qu’ils doivent utiliser les hello mot de passe local lorsque vous avez installé la connexion.

avertissement et la section précédente de hello en considération dans votre planification. Si vous avez apporté de nombreuses modifications dans Azure AD ne pas reflétée dans des locaux AD DS, vous devez tooplan comment toopopulate les services AD DS avec hello mise à jour de valeurs avant de synchroniser vos objets avec Azure AD Connect.

Si vous vos objets avec une correspondance de soft de correspondance, puis hello **sourceAnchor** est ajouté en toohello objet dans Azure AD pour une correspondance exacte peut être utilisée ultérieurement.

### <a name="hard-match-vs-soft-match"></a>Correspondance exacte et correspondance souple
Pour une nouvelle installation de Connect, il n’existe aucune différence pratique entre une correspondance souple et une correspondance exacte. différence de Hello est dans une situation de récupération d’urgence. Si votre serveur avec Azure AD Connect a connu une défaillance, vous pouvez réinstaller une nouvelle instance sans perdre de données. Un objet avec une ancre source est envoyé tooConnect lors de l’installation initiale. Hello correspondance peut être évaluée par client hello (Azure AD Connect), qui est beaucoup plus rapide que cette opération même hello dans Azure AD. Une correspondance exacte est évaluée à la fois par Connect et par Azure AD. Une correspondance souple n’est évaluée que par Azure AD.

### <a name="other-objects-than-users"></a>Objets autres que des utilisateurs
Les utilisateurs ont généralement userPrincipalName et proxyAddresses, ce qui facilite la correspondance de hello. Mais les autres objets, tels que les groupes de sécurité, n’ont pas ces attributs. Dans ce cas, vous pouvez uniquement en correspondance sur une correspondance exacte à l’aide de hello sourceAnchor. Hello sourceAnchor est toujours hello Base64 converti **objectGUID** localement, donc vous devez mettre à jour la valeur de hello dans Azure AD lorsque vous avez besoin de deux objets toomatch. Hello sourceAnchor/immutableID peuvent uniquement être mis à jour avec PowerShell et non par le biais des portails de hello.

## <a name="create-a-new-on-premises-active-directory-from-data-in-azure-ad"></a>Créer un nouveau répertoire Active Directory local à partir des données dans Azure AD
Certains clients démarrent avec une solution cloud uniquement avec Azure AD et ils ne disposent pas d’un répertoire AD local. Plus tard ils tooconsume des ressources locales et toobuild locale Active Directory en fonction des données d’Azure AD. Azure AD Connect ne peut pas vous aider dans ce scénario. Il ne crée pas les utilisateurs locaux et il n’a pas de n’importe quel toohello de capacité tooset hello mot de passe local même comme dans Azure AD.

Si la seule raison pour laquelle hello raison pour laquelle vous envisagez de tooadd local AD est toosupport LOB (Line-of-Business Applications), peut-être que vous devez envisager toouse [les services de domaine Active Directory Azure](../../active-directory-domain-services/index.md) à la place.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
