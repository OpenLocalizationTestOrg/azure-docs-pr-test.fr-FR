---
title: "aaaGet démarrée avec l’authentification Azure AD à l’aide de hello portail Azure | Documents Microsoft"
description: "Découvrez comment toouse hello tooaccess portail Azure tooconsume d’authentification Azure Active Directory (Azure AD) hello API Azure Media Services."
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a>Prise en main d’authentification Azure AD à l’aide de hello portail Azure

Découvrez comment toouse hello Azure tooaccess portail Azure Active Directory (Azure AD) d’authentification tooaccess hello API Azure Media Services.

## <a name="prerequisites"></a>Composants requis

- Un compte Azure. Si vous n’avez pas de compte, commencez avec un [essai gratuit Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Un compte Media Services. Pour plus d’informations, consultez [créer un compte Azure Media Services à l’aide de hello Azure portal](media-services-portal-create-account.md).
- Assurez-vous que vous passez en revue hello [l’accès à des API Azure Media Services avec une vue d’ensemble de l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

Lorsque vous utilisez l’authentification Azure AD avec Azure Media Services, vous disposez de deux options d’authentification :

- **Authentification utilisateur**. Authentifier un utilisateur de hello application toointeract avec les ressources de Media Services. les applications interactives Hello doivent tout d’abord utilisateur hello pour les informations d’identification. Un exemple est une application de console de gestion utilisée par les tâches d’encodage toomonitor des utilisateurs autorisés ou la diffusion en continu. 
- **Authentification d’un principal de service**. Authentifiez un service. Les applications qui utilisent généralement cette méthode d’authentification sont des applications qui exécutent des services démon, des services de niveau intermédiaire ou des travaux planifiés : applications web, applications de fonction, applications logiques, API ou microservices.

> [!IMPORTANT]
> Actuellement, Media Services prend en charge le modèle d’authentification hello Azure Access Control service. Toutefois, l’autorisation Access Control sera déconseillée à compter du 1er juin 2018. Nous vous recommandons de migrer modèle d’authentification Azure AD de toohello dès que possible.

## <a name="select-hello-authentication-method"></a>Sélectionnez la méthode d’authentification hello

1. Bonjour [portail Azure](https://portal.azure.com/), sélectionnez votre compte Media Services.
2. Sélectionnez la façon dont tooconnect toohello API Media Services.

    ![Sélectionner la page de méthode de connexion](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a>Authentification utilisateur

tooconnect toohello API Media Services à l’aide de hello option d’authentification utilisateur, hello client application doit toorequest un jeton d’Azure AD a hello paramètres suivants :  

* Point de terminaison de locataire Azure AD
* URI de ressource Media Services
* ID client d’application Media Services (natif) 
* URI de redirection d’application Media Services (natif) 
* URI de ressource pour REST Media Services

Vous pouvez obtenir les valeurs hello pour ces paramètres sur hello **API Media Services avec l’authentification utilisateur** page. 

![Se connecter à la page d’authentification utilisateur](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

Si vous vous connectez toohello API Media Services à l’aide de hello Media Services Microsoft .NET SDK, hello requis valeurs tooyou disponible en tant que partie du Kit de développement logiciel de hello. Pour plus d’informations, consultez [utilisent Azure AD authentication tooaccess hello API Azure Media Services avec .NET](media-services-dotnet-get-started-with-aad.md).

Si vous n’utilisez pas le client de Media Services .NET hello SDK, vous devez créer manuellement une demande de jeton Azure AD à l’aide de paramètres hello abordées précédemment. Pour plus d’informations, consultez [comment toouse hello Azure AD Authentication Library tooget hello jeton Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="service-principal-authentication"></a>Authentification d’un principal du service

tooconnect toohello API Media Services à l’aide de hello option principal de service, votre application de couche intermédiaire (API web ou une application web) doit toorequest un jeton d’Azure AD a hello paramètres suivants :  

* Point de terminaison de locataire Azure AD
* URI de ressource Media Services 
* URI de ressource pour REST Media Services
* Valeurs de l’application Azure AD : hello **ID client** et **question secrète du client**

Vous pouvez obtenir les valeurs hello pour ces paramètres sur hello **Rejoignez tooMedia API des Services de principal du service** page. Utilisez cette page de toocreate un nouvel Azure application AD ou tooselect un existant. Après avoir sélectionné des application Azure AD de hello, vous pouvez obtenir l’ID de client hello (ID d’Application) et générer des valeurs de clé secrète (clé) de client hello. 

![Se connecter à la page du principal de service](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

Hello lorsque **Principal du Service** panneau s’ouvre, l’application Azure AD première hello répondant hello suivant des critères est activée :

- Il s’agit d’une application Azure AD inscrite.
- Il dispose d’autorisations de collaborateur ou Owner Role-Based le contrôle d’accès sur le compte de hello.

Une fois que vous créez ou sélectionnez une application Azure AD, vous pouvez créer et copier une question secrète du client (clé) et hello client ID (ID d’Application). l’ID de client et de la clé secrète du client Hello sont un jeton d’accès hello tooget requis dans ce scénario.

Si vous n’avez pas applications Azure AD de toocreate autorisations dans votre domaine, les contrôles d’application Azure AD hello du Panneau de hello ne sont pas affichés, et un message d’avertissement s’affiche.

Si vous vous connectez toohello API Media Services à l’aide de hello Media Services .NET SDK, consultez [utilisent Azure AD authentication tooaccess hello API Azure Media Services avec .NET](media-services-dotnet-get-started-with-aad.md).

Si vous n’utilisez pas de client de Media Services .NET hello SDK, vous devez créer manuellement une demande de jeton Azure AD à l’aide de paramètres hello abordées précédemment. Pour plus d’informations, consultez [comment toouse hello Azure AD Authentication Library tooget hello jeton Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="get-hello-client-id-and-client-secret"></a>Obtenir les client hello client et le code secret

Après avoir sélectionné une application Azure AD existante hello sélectionnez option toocreate un nouveau, hello suivant boutons s’affichent :

![Bouton Gérer les autorisations et bouton Gérer l’application](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

tooopen hello panneau des applications Azure AD, cliquez sur **gérer application**. Sur hello **gérer application** panneau, vous pouvez obtenir un ID de client de l’application hello (ID d’Application). toogenerate une clé secrète client (clé), sélectionnez **clés**.

![Option Clés du panneau Gérer l’application](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a>Gérer les autorisations et l’application hello

Après avoir sélectionné des application Azure AD de hello, vous pouvez gérer les autorisations et l’application hello. tooset votre tooaccess d’application Azure AD d’autres applications, cliquez sur **gérer les autorisations**. Pour les tâches de gestion, telles que la modification des clés et les URL de réponse ou tooedit hello du manifeste d’application, cliquez sur **gérer application**.

### <a name="edit-hello-apps-settings-or-manifest"></a>Modifier les paramètres de l’application hello ou le manifeste.

paramètres d’application tooedit hello ou de manifeste, cliquez sur **gérer application**.

![Page Gérer l’application](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a>Étapes suivantes

Prise en main [téléchargement de fichiers tooyour compte](media-services-portal-upload-files.md).
