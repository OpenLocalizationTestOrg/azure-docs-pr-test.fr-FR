---
title: "les applications prenant en charge les aaaClaims - Proxy d’application Azure AD | Documents Microsoft"
description: "Comment toopublish localement les applications ASP.NET qui accepte les revendications AD FS pour l’accès à distance sécurisé par vos utilisateurs."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a>Utilisation d’applications prenant en charge les revendications dans le proxy d’application
[Les applications prenant en charge les revendications](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) effectuer une redirection de toohello Service de jeton de sécurité (STS). Hello STS demande des informations d’identification d’utilisateur hello en échange d’un jeton et redirige ensuite l’application hello utilisateur toohello. Il existe quelques toowork de Proxy d’Application tooenable manières avec ces redirections. Utilisez cette tooconfigure article votre déploiement pour les applications prenant en charge les revendications. 

## <a name="prerequisites"></a>Composants requis
Assurez-vous que ce STS hello qui hello application prenant en charge les revendications redirige toois disponible en dehors de votre réseau local. Vous pouvez rendre hello STS disponible en exposant via un proxy ou en autorisant les connexions à l’extérieur. 

## <a name="publish-your-application"></a>Publication de votre application

1. Publier votre application en fonction des instructions toohello décrites dans [publier des applications avec Proxy d’Application](application-proxy-publish-azure-portal.md).
2. Parcourir la page d’application toohello Bonjour portail et sélectionnez **l’authentification unique**.
3. Si vous choisissez **Azure Active Directory** comme **méthode de préauthentification**, sélectionnez **Authentification unique Azure AD désactivée** comme **méthode d’authentification interne**. Si vous avez choisi **Passthrough** en tant que votre **méthode de pré-authentification**, vous n’avez pas besoin toochange n’est pas défini.

## <a name="configure-adfs"></a>Configurer AD FS

Vous pouvez configurer AD FS pour les applications prenant en charge les revendications de deux façons. Hello est tout d’abord à l’aide de domaines personnalisés. Hello est ensuite avec WS-Federation. 

### <a name="option-1-custom-domains"></a>Option 1 : domaines personnalisés

Si tous hello URL internes pour vos applications sont pleinement qualifiées (FQDN) des noms de domaine, vous pouvez ensuite configurer [des domaines personnalisés](active-directory-application-proxy-custom-domains.md) pour vos applications. Utilisez hello domaines personnalisés toocreate URL externes qui sont hello identique hello URL internes. Lorsque votre URL externes correspondent à votre URL internes, les redirections de STS hello fonctionnent si vos utilisateurs sont en local ou à distance. 

### <a name="option-2-ws-federation"></a>Option 2 : WS-Federation

1. Ouvrez Gestion AD FS.
2. Accédez trop**confiance**, avec le bouton droit sur l’application hello publication avec le Proxy d’Application, puis choisissez **propriétés**.  

   ![Approbations de partie de confiance, clic droit sur le nom de l’application - capture d’écran](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. Sur hello **points de terminaison** sous l’onglet sous **type de point de terminaison**, sélectionnez **WS-Federation**.
4. Sous **URL de confiance**, entrez les URL hello saisis dans hello Proxy d’Application sous **URL externe** et cliquez sur **OK**.  

   ![Ajouter un point de terminaison, définition de la valeur de l’URL approuvée – capture d’écran](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a>Étapes suivantes
* [Activer l’authentification unique](application-proxy-sso-overview.md) pour les applications qui ne prennent pas en charge les revendications
* [Activer toointeract d’applications client natif avec les applications du proxy](active-directory-application-proxy-native-client.md)


