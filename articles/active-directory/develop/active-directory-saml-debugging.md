---
title: "Débogage d’une authentification unique basée sur SAML aux applications dans Azure Active Directory | Microsoft Docs"
description: "Découvrez comment déboguer une authentification unique basée sur SAML aux applications dans Azure Active Directory  "
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
ms.openlocfilehash: 31447d597296bac57481dc2acb4a95ee3a104161
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-debug-saml-based-single-sign-on-to-applications-in-azure-active-directory"></a>Débogage d’une authentification unique basée sur SAML aux applications dans Azure Active Directory
Lors du débogage d’une intégration d'application basée sur SAML, il est généralement conseillé d'utiliser un outil tel que [Fiddler](http://www.telerik.com/fiddler) pour afficher la requête SAML, la réponse SAML et le jeton SAML actuel émis à l'application. En examinant le jeton SAML, vous pouvez vous assurer que tous les attributs requis, le nom d'utilisateur dans l'objet SAML et l'URI de l'émetteur vous parviennent comme prévu.

![][1]

La réponse d'Azure AD qui contient le jeton SAML est généralement celle qui est générée après une redirection HTTP 302 depuis https://login.windows.net et qui est envoyée à **l’URL de réponse** configurée de l'application. 

Vous pouvez afficher le jeton SAML en sélectionnant cette ligne, puis l’onglet **Inspecteurs > WebForms** dans le volet droit. À partir de là, cliquez sur la valeur **SAMLResponse** et sélectionnez **Send to TextWizard**. Puis sélectionnez **From Base64** à partir du menu **Transform** pour décoder le jeton et afficher son contenu.

**Remarque**: pour afficher le contenu de cette requête HTTP, Fiddler peut vous inviter à configurer le déchiffrement du trafic HTTPS, que vous devez effectuer.

## <a name="related-articles"></a>Articles connexes
* [Index d’articles pour la gestion des applications dans Azure Active Directory](../active-directory-apps-index.md)
* [Configuration de l'authentification unique pour les applications ne faisant pas partie de la galerie d'applications Azure Active Directory.](../active-directory-saas-custom-apps.md)
* [Personnalisation des revendications émises dans le jeton SAML pour les applications pré-intégrées](active-directory-saml-claims-customization.md)

<!--Image references-->
[1]: ../media/active-directory-saml-debugging/fiddler.png