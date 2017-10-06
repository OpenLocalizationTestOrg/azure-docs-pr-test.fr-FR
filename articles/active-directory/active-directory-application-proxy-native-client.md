---
title: "applications clientes natives d’aaaPublish - Azure AD | Documents Microsoft"
description: "Décrit comment tooenable native client applications toocommunicate avec tooyour de sécuriser l’accès à distance de connecteur Proxy d’Application Azure AD tooprovide localement les applications."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a>Comment tooenable native client applications toointeract avec le proxy d’Applications

Dans les applications tooweb addition, Proxy d’Application Azure Active Directory peut également être utilisé toopublish native client applications. Les applications clientes natives sont différentes des applications web du fait qu’elles sont installées sur un appareil alors que les applications web sont accessibles via un navigateur. 

Le proxy d’application prend en charge les applications clientes natives en acceptant les jetons générés par Azure AD qui sont envoyés dans des en-têtes d’autorisation HTTP standard.

![Relation entre les utilisateurs finaux, Azure Active Directory et les applications publiées](./media/active-directory-application-proxy-native-client/richclientflow.png)

Utilisez hello Azure bibliothèque d’authentification Active Directory, qui prend en charge l’authentification et prend en charge de nombreux environnements clients, les applications natives toopublish. Le Proxy d’application s’adapte à hello [scénario de tooWeb API Application Native](develop/active-directory-authentication-scenarios.md#native-application-to-web-api). Cet article vous guide tout au long des quatre étapes de hello toopublish une application native avec le Proxy d’Application et hello bibliothèque d’authentification Azure AD. 

## <a name="step-1-publish-your-application"></a>Étape 1 : publier votre application
Publier votre application proxy comme vous le feriez pour toute autre application et affecter des utilisateurs tooaccess votre application. Pour plus d'informations, consultez [Publier des applications avec le proxy d'application](active-directory-application-proxy-publish.md).

## <a name="step-2-configure-your-application"></a>Étape 2 : configurer votre application
Configurez votre application native comme suit :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Accédez trop**Azure Active Directory** > **inscriptions d’application**.
3. Sélectionnez **Nouvelle inscription d’application**.
4. Spécifiez un nom pour votre application, sélectionnez **natif** en tant que type d’application hello et fournir hello URI de redirection pour votre application. 

   ![Créer une nouvelle inscription d’application](./media/active-directory-application-proxy-native-client/create.png)
5. Sélectionnez **Créer**.

Pour plus d’informations sur la création d’une nouvelle inscription d’application, consultez [Integrating applications with Azure Active Directory](.//develop/active-directory-integrating-applications.md) (Intégration d’applications à Azure Active Directory).


## <a name="step-3-grant-access-tooother-applications"></a>Étape 3 : Applications de tooother accorder l’accès
Permettre aux applications hello application native toobe exposée tooother dans votre répertoire :

1. Toujours dans **inscriptions d’application**, sélectionnez hello nouvelle application native que vous venez de créer.
2. Sélectionnez **Autorisations requises**.
3. Sélectionnez **Ajouter**.
4. Première étape de hello ouvert, **sélectionner une API**.
5. Utilisez hello barre toofind hello Proxy d’Application application de recherche que vous avez publiée dans la première section de hello. Choisissez cette application, puis cliquez sur **Sélectionner**. 

   ![Recherche de l’application de proxy hello](./media/active-directory-application-proxy-native-client/select_api.png)
6. Deuxième étape de hello ouvert, **sélectionner les autorisations**.
7. Toogrant de case à cocher hello votre application proxy d’application native accès tooyour, puis cliquez sur **sélectionnez**.

   ![Application de tooproxy grant access](./media/active-directory-application-proxy-native-client/select_perms.png)
8. Sélectionnez **Terminé**.


## <a name="step-4-edit-hello-active-directory-authentication-library"></a>Étape 4 : Modifier hello bibliothèque d’authentification Active Directory
Modifier le code de l’application native hello dans le contexte d’authentification hello Hello de tooinclude hello Active Directory Authentication Library (ADAL) après le texte :

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

variables Hello dans l’exemple de code hello doivent être remplacés comme suit :

* **ID de locataire** se trouvent dans hello portail Azure. Accédez trop**Azure Active Directory** > **propriétés** et copie Bonjour ID de répertoire. 
* **URL externe** est hello frontal URL est saisie Bonjour Proxy d’Application. toofind cette valeur, accédez toohello **le proxy d’Application** section de l’application de proxy hello.
* **ID d’application** Hello application native se trouvent sur hello **propriétés** page de l’application native hello.
* **URI de redirection de l’application native hello** se trouvent sur hello **URI de redirection** page de l’application native hello.


## <a name="see-also"></a>Voir aussi

Pour plus d’informations sur les flux de l’application native hello, consultez [application Native tooweb API](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)

Pour les informations les plus récentes hello et mises à jour, consultez hello [blog de Proxy d’Application](http://blogs.technet.com/b/applicationproxyblog/)
