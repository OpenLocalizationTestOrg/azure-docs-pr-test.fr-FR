---
title: "aaaListing votre application dans la galerie d’applications Azure Active Directory hello"
description: "Comment toolist une application qui prend en charge l’authentification unique dans hello Galerie d’Azure Active Directory | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a>Affichage de votre application dans la galerie d’applications Azure Active Directory hello
une application qui prend en charge l’authentification unique sur avec Azure Active Directory Bonjour de toolist [Galerie d’Azure AD](https://azure.microsoft.com/marketplace/active-directory/all/), application hello doit tout d’abord une tooimplement Hello suivant des modes d’intégration :

* **OpenID Connect** - intégration directe avec Azure AD en utilisant OpenID Connect pour l’authentification et hello consentement d’Azure AD API pour la configuration. Si vous commencez une intégration et votre application ne prend pas en charge SAML, il s’agit de mode de recommandation hello.
* **SAML** : votre application a déjà des fournisseurs d’identité tiers hello capacité tooconfigure à l’aide du protocole SAML de hello.

Les exigences pour chaque mode sont indiquées ci-dessous.

## <a name="openid-connect-integration"></a>Intégration d'OpenID Connect
toointegrate votre application auprès d’Azure AD, hello suivant [les instructions de développeur](active-directory-authentication-scenarios.md). Répondez aux questions de hello ci-dessous, puis envoyer toowaadpartners@microsoft.com.

* Fournissez les informations d’identification pour un compte ou un client de test avec l’application qui peut être utilisée par hello intégration d’Azure AD équipe tootest hello.  
* Fournissent des instructions sur l’équipe de hello Azure AD peut se connecter et se connecter à une instance de l’application de tooyour Azure AD à l’aide de hello [infrastructure de consentement d’Azure AD](active-directory-integrating-applications.md#overview-of-the-consent-framework). 
* Fournir des instructions supplémentaires requises pour hello Azure AD de l’équipe tootest single sign-on avec votre application. 
* Spécifiez les informations de hello ci-dessous :

> Nom de l’entreprise :
> 
> Site web de l’entreprise :
> 
> Nom de l’application :
> 
> Description de l’application (200 caractères maximum) :
> 
> Site web de l’application (pour informatif) :
> 
> Site web du support technique de l’application ou les informations de contact :
> 
> ID d’application de l’application hello, comme indiqué dans les détails de l’application hello à https://portal.azure.com :
> 
> URL d’inscription de l’application où les clients vont toosign pour et et/ou d’achat application hello :
> 
> Choisissez les catégories de toothree pour votre toobe application répertoriés sous (pour les catégories disponibles voir hello Azure Active Directory Marketplace) :
> 
> Attacher une petite icône d’application (fichier PNG, 45 px par 45 px, couleur d’arrière-plan unie) :
> 
> Attacher une grande icône d’application (fichier PNG, 215 px par 215 px, couleur d’arrière-plan unie) :
> 
> Attacher un grand logo d’application (fichier PNG, 150 px par 122 px, couleur d’arrière-plan unie) :
> 
> 

## <a name="saml-integration"></a>Intégration de SAML
N’importe quelle application qui prend en charge SAML 2.0 peut être intégrée directement à un locataire Azure AD à l’aide de [ces tooadd instructions une application personnalisée](../active-directory-saas-custom-apps.md). Une fois que vous avez testé que votre intégration d’application fonctionne avec Azure AD, envoyer hello informations suivantes trop<mailto:waadpartners@microsoft.com>.

* Fournissez les informations d’identification pour un compte ou un client de test avec l’application qui peut être utilisée par hello intégration d’Azure AD équipe tootest hello.  
* Fournir hello SAML URL de connexion, URL de l’émetteur (ID d’entité), et l’URL de réponse (service de consommateur d’assertion) valeurs pour votre application, comme indiqué [ici](../active-directory-saas-custom-apps.md). Si vous fournissez généralement ces valeurs dans un fichier de métadonnées SAML, envoyez également ce dernier.
* Fournissent une brève description de la façon tooconfigure Azure AD comme fournisseur d’identité dans votre application à l’aide de SAML 2.0. Si votre application prend en charge la configuration d’Azure AD comme fournisseur d’identité via un portail administratif libre-service, puis vérifiez que les informations d’identification de hello fournies ci-dessus incluent hello capacité tooset cette installation.
* Spécifiez les informations de hello ci-dessous :

> Nom de l’entreprise :
> 
> Site web de l’entreprise :
> 
> Nom de l’application :
> 
> Description de l’application (200 caractères maximum) :
> 
> Site web de l’application (pour informatif) :
> 
> Site web du support technique de l’application ou les informations de contact :
> 
> URL d’inscription de l’application où les clients vont toosign pour et et/ou d’achat application hello :
> 
> Choisissez les catégories de toothree pour votre toobe application répertoriés sous (pour les catégories disponibles, consultez hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))) :
> 
> Attacher une petite icône d’application (fichier PNG, 45 px par 45 px, couleur d’arrière-plan unie) :
> 
> Attacher une grande icône d’application (fichier PNG, 215 px par 215 px, couleur d’arrière-plan unie) :
> 
> Attacher un grand logo d’application (fichier PNG, 150 px par 122 px, couleur d’arrière-plan unie) :
> 
> 

