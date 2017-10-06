---
title: "aaaHow toodebug basé sur SAML uniques authentification tooapplications dans Azure Active Directory | Documents Microsoft"
description: "Découvrez comment toodebug basé sur SAML uniques authentification tooapplications dans Azure Active Directory "
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: edbe492b-1050-4fca-a48a-d1fa97d47815
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.custom: aaddev
ms.reviewer: dastrock
ms.openlocfilehash: 846c7b3497c8842947c5b406f4362b9e06785b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-saml-based-single-sign-on-tooapplications-in-azure-active-directory"></a>Comment toodebug basé sur SAML uniques authentification tooapplications dans Azure Active Directory
Lors du débogage d’une intégration d’application basée sur SAML, il est souvent utile toouse un outil tel que [Fiddler](http://www.telerik.com/fiddler) toosee hello demande SAML, réponse SAML hello et hello réel jeton SAML qui est émise toohello application. En examinant le jeton SAML de hello, vous pouvez vous assurer que tous les hello attributs requis, hello nom d’utilisateur dans l’objet SAML hello et hello émetteur URI arrivent via comme prévu.

![][1]

Hello réponse Azure AD, qui contient le jeton SAML de hello est généralement hello qui a lieu après une redirection HTTP 302 de https://login.windows.net et toohello envoyé n’est configuré **URL de réponse** de l’application hello. 

Vous pouvez afficher le jeton SAML de hello en sélectionnant cette ligne, puis en sélectionnant hello **inspecteurs > WebForms** onglet dans le panneau droit hello. À partir de là, avec le bouton droit hello **SAMLResponse** valeur et sélectionnez **envoyer tooTextWizard**. Puis sélectionnez **à partir de Base64** de hello **transformer** menu toodecode hello jeton et afficher son contenu.

**Remarque**: demande de contenu de hello toosee cette HTTP, Fiddler peut vous demander de déchiffrement tooconfigure du trafic HTTPS, vous devez toodo.

## <a name="related-articles"></a>Articles connexes
* [Index d’articles pour la gestion des applications dans Azure Active Directory](../active-directory-apps-index.md)
* [Configuration uniques tooapplications ouverture de session qui ne sont pas dans la galerie d’applications Azure Active Directory hello](../active-directory-saas-custom-apps.md)
* [Comment tooCustomize les revendications émises dans hello du jeton SAML pour les applications Pre-Integrated](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png