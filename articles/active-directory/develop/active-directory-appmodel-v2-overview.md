---
title: point de terminaison aaaAzure Active Directory v2.0 | Documents Microsoft
description: "Une présentation toobuilding des applications avec Microsoft Account et Azure Active Directory connectez-vous."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a>Connecter les utilisateurs de compte Microsoft et d’Azure AD dans une même application
Bonjour passé, un développeur d’application qui voulaient toosupport les deux comptes personnels de Microsoft et des comptes à partir d’Azure Active Directory a été toointegrate requise avec deux systèmes distincts.  Hello **point de terminaison Azure AD v2.0** introduit une nouvelle version d’API d’authentification qui vous permet de toosign dans les deux types de comptes à l’aide d’une intégration simple.  Applications qui utilisent le point de terminaison hello v2.0 peuvent également consommer API REST hello [Microsoft Graph](https://graph.microsoft.io) à l’aide d’un type de compte.

## <a name="getting-started"></a>Mise en route
Choisissez votre plateforme favoris hello suivant liste toobuild une application à l’aide de notre bibliothèques open source et les infrastructures.  Vous pouvez également utiliser notre toosend de documentation de protocole OAuth 2.0 et OpenID Connect et recevoir des messages de protocole directement sans l’aide d’une bibliothèque d’authentification.

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a>Nouveautés
informations Hello ici seront utiles pour comprendre ce qui est et ce qui n’est pas possible avec le point de terminaison hello v2.0.

* En savoir plus sur hello [types d’applications que vous pouvez générer avec le point de terminaison hello v2.0](active-directory-v2-flows.md).
* Comprendre hello [limitations, les restrictions et les contraintes](active-directory-v2-limitations.md) avec point de terminaison hello v2.0.
* Consultez cette présentation vidéo de point de terminaison hello v2.0 :

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a>Référence
Ces liens peuvent être utiles pour l’exploration de plateforme hello en profondeur :

* [Référence sur le protocole v2.0](active-directory-v2-protocols.md)
* [Référence sur le jeton v2.0](active-directory-v2-tokens.md)
* [Référence de la bibliothèque v2.0](active-directory-v2-libraries.md)
* [Étendues et consentement dans le point de terminaison hello v2.0](active-directory-v2-scopes.md)
* [Hello Microsoft Graph](https://graph.microsoft.io)

## <a name="help--support"></a>Aide et support
Il s’agit hello meilleurs emplacements tooget aide avec le développement sur Azure Active Directory.

* [Balises `azure-active-directory` et `adal` de Stack Overflow](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [Commentaires sur Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> Si vous devez uniquement toosign dans des comptes professionnels et scolaires à partir d’Azure Active Directory, vous devez commencer par notre [guide du développeur Azure AD](active-directory-developers-guide.md).  point de terminaison Hello v2.0 est destiné à être utilisé par les développeurs qui doivent explicitement toosign dans des comptes personnels Microsoft.

