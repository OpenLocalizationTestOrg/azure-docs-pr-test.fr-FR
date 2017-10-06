---
title: "Azure Active Directory B2C : inscription d’application | Microsoft Docs"
description: Comment tooregister votre application avec Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: PatAltimore
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f69
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: parakhj
ms.openlocfilehash: bd58e123751db387d6c8f16bd010291ba698b1a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-register-your-application"></a>Azure Active Directory B2C : inscription de votre application

Ce démarrage rapide vous aide à inscrire une application dans un client B2C Microsoft Azure Active Directory (Azure AD) en quelques minutes. Lorsque vous avez terminé, votre application est enregistrée pour une utilisation dans le locataire de hello Azure B2C.

## <a name="prerequisites"></a>Composants requis

toobuild une application qui accepte le consommateur d’inscription et de connexion, vous devez tout d’abord d’application de hello tooregister avec un locataire Azure Active Directory B2C. Obtenir votre propre locataire à l’aide de hello étapes [créer un client Azure AD B2C](active-directory-b2c-get-started.md).

Les applications créées à partir du panneau hello Azure AD B2C Bonjour portail Azure doivent être gérées à partir de hello même emplacement. Si vous modifiez les applications B2C hello à l’aide de PowerShell ou un autre portail, ils deviennent non pris en charge et ne fonctionnent pas avec Azure Active Directory B2C. Consultez les détails dans hello [a généré une erreur d’applications](#faulted-apps) section. 

## <a name="navigate-toob2c-settings"></a>Accédez tooB2C paramètres

Connectez-vous à toohello [portail Azure](https://portal.azure.com/) comme hello administrateur Global du client de hello B2C. 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../../includes/active-directory-b2c-switch-b2c-tenant.md)]

[!INCLUDE [active-directory-b2c-portal-navigate-b2c-service](../../includes/active-directory-b2c-portal-navigate-b2c-service.md)]

Choisissez les étapes suivantes, selon le type d’application hello que l’inscription :

* [Inscrire une application web](#register-a-web-app)
* [Inscrire une API web](#register-a-web-api)
* [Inscrire une application mobile ou native](#register-a-mobile-or-native-app)
 
## <a name="register-a-web-app"></a>Inscrire une application web

[!INCLUDE [active-directory-b2c-register-web-app](../../includes/active-directory-b2c-register-web-app.md)]

Si votre application web appelle une API web sécurisée par Azure AD B2C, procédez comme suit :
   1. Créer un secret d’application en accédant de toohello **clés** lame et en cliquant sur hello **générer une clé** bouton. Prenez note de hello **clé application** valeur. Vous utilisez les valeur hello en tant que secret d’application hello dans le code de votre application.
   2. Cliquez sur **Accès d’API**, cliquez sur **Ajouter**, puis sélectionnez votre API web et les étendues (autorisations).

> [!NOTE]
> Une **Clé secrète d’application** est une information d’identification de sécurité importante, qui doit être correctement sécurisée.
> 

[Raccourcis trop**étapes suivantes**](#next-steps)

## <a name="register-a-web-api"></a>Inscrire une API web

[!INCLUDE [active-directory-b2c-register-web-api](../../includes/active-directory-b2c-register-web-api.md)]

Cliquez sur **publié étendues** tooadd plus étendues en fonction des besoins. Par défaut, l’étendue hello « user_impersonation » est défini. l’étendue user_impersonation Hello donne aux autres tooaccess de capacité hello applications Cette api pour le compte d’utilisateur connecté hello. Si vous le souhaitez, l’étendue user_impersonation hello peut être supprimée.

[Raccourcis trop**étapes suivantes**](#next-steps)

## <a name="register-a-mobile-or-native-app"></a>Inscrire une application mobile/native

[!INCLUDE [active-directory-b2c-register-mobile-native-app](../../includes/active-directory-b2c-register-mobile-native-app.md)]

[Raccourcis trop**étapes suivantes**](#next-steps)

## <a name="limitations"></a>Limites

### <a name="choosing-a-web-app-or-api-reply-url"></a>Choix d’une URL de réponse d’API ou d’application web

Actuellement, les applications qui sont inscrits auprès d’Azure AD B2C sont ensemble restreint tooa limité de valeurs d’URL de réponse. Hello réponse URL pour les services et applications web doit commencer par le schéma de hello `https`, et répondent à toutes les valeurs d’URL doivent partager un seul domaine DNS. Par exemple, vous ne pouvez pas inscrire une application web comportant l’une des URL de réponse suivantes :

`https://login-east.contoso.com`

`https://login-west.contoso.com`

système d’enregistrement de Hello compare hello ensemble nom DNS de hello existant réponse URL toohello nom DNS de l’URL de réponse hello que vous ajoutez. tooadd hello nom DNS de Hello demande échoue si une de hello conditions suivantes est vraie :

* nom DNS complet de Hello hello nouvelle URL de réponse ne correspond pas de nom DNS de hello hello existant URL de réponse.
* nom DNS complet de Hello hello nouvelle URL de réponse n’est pas un sous-domaine de l’URL de réponse existante hello.

Par exemple, si hello app a cette URL de réponse :

`https://login.contoso.com`

Vous pouvez ajouter tooit, comme suit :

`https://login.contoso.com/new`

Dans ce cas, le nom DNS de hello correspond exactement. Vous pouvez aussi définir l’URI suivant :

`https://new.login.contoso.com`

Dans ce cas, vous faites référence sous-domaine DNS de tooa de login.contoso.com. Si vous souhaitez toohave une application ayant east.contoso.com de connexion et de connexion-west.contoso.com comme URL de réponse, vous devez ajouter les URL de réponse dans cet ordre :

`https://contoso.com`

`https://login-east.contoso.com`

`https://login-west.contoso.com`

Vous pouvez ajouter hello deux derniers étant sous-domaines hello première URL de réponse, contoso.com.

### <a name="choosing-a-native-app-redirect-uri"></a>Choix d’un URI de redirection d’application native

Il existe deux points importants à prendre en considération lors du choix d’un URI de redirection pour les applications mobiles/natives :

* **Unique**: schéma hello de l’URI de redirection hello doit être unique pour chaque application. Dans notre exemple (com.onmicrosoft.contoso.appname://redirect/path), nous utilisons com.onmicrosoft.contoso.appname en tant que schéma de hello. Nous vous recommandons de suivre ce modèle. Si les deux applications partagent hello même schéma, hello utilisateur voit une boîte de dialogue « Choisir l’application ». Si l’utilisateur de hello effectue un choix incorrect, la connexion de hello échoue.
* **Complet** : l’URI de redirection doit comporter un schéma et un chemin d’accès. chemin d’accès Hello doit contenir au moins une barre oblique (par exemple, //contoso/ fonctionne et //contoso échoue) du domaine hello.

N’Assurez-vous aucun des caractères spéciaux tels que l’uri de redirection des traits de soulignement dans hello.

### <a name="faulted-apps"></a>Applications ayant généré une erreur

Les applications B2C ne doivent PAS être modifiées :

* Sur les autres portails de gestion des applications tels que le [Portail Azure Classic](https://manage.windowsazure.com/) et le [Portail d’inscription des applications](https://apps.dev.microsoft.com/)
* À l’aide de l’API Graph ou de PowerShell

Si vous modifiez l’application hello B2C comme décrit ci-dessus et tooedit à nouveau dans le panneau de fonctionnalités hello Azure AD B2C sur hello portail Azure, elle devient une application ayant généré une erreur, et votre application n’est plus utilisable avec Azure Active Directory B2C. Vous avez toodelete hello application et créez un nouveau.

application de hello toodelete, accédez toohello [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/) et supprimer l’application hello. Toobe d’application hello visible, vous devez propriétaire hello toobe application hello (et pas seulement à un administrateur de client de hello).

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez une application inscrite auprès de Azure AD B2C, vous pouvez effectuer l’une de [nos didacticiels de démarrage rapide](active-directory-b2c-overview.md#get-started) tooget haut et en cours d’exécution.

> [!div class="nextstepaction"]
> [Créer une application web ASP.NET avec inscription, connexion et réinitialisation de mot de passe](active-directory-b2c-devquickstarts-web-dotnet-susi.md)