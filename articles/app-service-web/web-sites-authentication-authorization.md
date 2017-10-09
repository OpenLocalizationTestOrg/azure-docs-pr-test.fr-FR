---
title: aaaAuthenticate avec Active Directory locale dans votre application Azure | Documents Microsoft
description: "En savoir plus sur les différentes options de hello pour les applications line-of-business dans tooauthenticate Azure App Service avec Active Directory local"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
ms.assetid: dde6b7e6-bf6a-4fa5-8390-3a18155d21bd
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 08/31/2016
ms.author: cephalin
ms.openlocfilehash: 65bf25aaa0447fbbea7c754db55842d57e70757e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-on-premises-active-directory-in-your-azure-app"></a>Authentification avec Active Directory en local dans votre application Azure
Cet article vous explique comment tooauthenticate avec locale Active Directory (AD) dans [Azure App Service](../app-service/app-service-value-prop-what-is.md). Une application Azure est hébergée dans le cloud de hello, mais il existe des méthodes tooauthenticate AD utilisateurs locaux en toute sécurité. 

## <a name="authenticate-through-azure-active-directory"></a>S’authentifier via Azure Active Directory
Un client Azure Active Directory peut être synchronisé avec un annuaire Active Directory local. Cette approche permet aux utilisateurs d’accéder à votre application à partir d’AD hello internet et de s’authentifier à l’aide de leurs informations d’identification locales. En outre, Azure App Service fournit une [solution clé en main pour cette méthode](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). En quelques clics, vous pouvez activer l’authentification avec un client synchronisé avec l’annuaire pour votre application Azure. Cette approche présente hello suivant avantages :

* Ne nécessite pas de code d’authentification dans votre application. Permettent de Service de l’application, procédez hello d’authentification et de temps sur la fourniture de fonctionnalités dans votre application.
* [API Azure AD Graph](http://msdn.microsoft.com/library/azure/hh974476.aspx) permet d’accéder aux données de toodirectory à partir de votre application Azure.
* Fournit l’authentification unique trop[toutes les applications prises en charge par Azure Active Directory](/marketplace/active-directory/), notamment Office 365, Dynamics CRM Online, Microsoft Intune et des milliers d’applications de cloud non Microsoft. 
* Azure Active Directory prend en charge le contrôle d’accès en fonction du rôle Azure Active Directory. Vous pouvez utiliser le modèle de hello [Authorize(Roles="X")] avec le code de tooyour des modifications minimes.

toosee toowrite une application Azure de métier qui s’authentifie auprès d’Azure Active Directory, voir [créer une application Azure line-of-business avec authentification Azure Active Directory](web-sites-dotnet-lob-application-azure-ad.md).

## <a name="authenticate-through-an-on-premises-sts"></a>S’authentifier via un service STS local
Si vous avez un local sécurisé jeton service (STS), comme les Services de fédération Active Directory (AD FS), vous pouvez utiliser l’authentification toofederate pour votre application Azure. Cette approche est recommandée lorsque la stratégie d’entreprise interdit le stockage de données AD dans Azure. Toutefois, notez les suivant hello :

* La topologie des services STS doit être déployée localement, ce qui implique une surcharge de gestion et de coût.
* Seuls les administrateurs de services AD FS peuvent configurer [de partie de confiance approbations de tiers et les règles de revendication](http://technet.microsoft.com/library/dd807108.aspx), ce qui peut limiter les options du développeur hello. Sur hello autre part, il est possible de toomanage et personnaliser [revendications](http://technet.microsoft.com/library/ee913571.aspx) sur chaque application.
* Accéder au site tooon données Active Directory requièrent une solution distincte à travers le pare-feu d’entreprise hello.

toosee toowrite une application Azure de métier qui s’authentifie auprès d’un STS local, voir [créer une application Azure line-of-business avec authentification AD FS](web-sites-dotnet-lob-application-adfs.md).

