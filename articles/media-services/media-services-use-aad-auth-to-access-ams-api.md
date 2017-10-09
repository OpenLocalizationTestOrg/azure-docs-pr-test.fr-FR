---
title: "aaaAccess API Azure Media Services avec l’authentification Azure Active Directory | Documents Microsoft"
description: "Découvrez les concepts et les étapes tootake toouse Azure Active Directory (Azure AD) tooauthenticate accès toohello API Azure Media Services."
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
ms.openlocfilehash: bb8f75f39100dc37098260c24ab4a199ef689d46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-hello-azure-media-services-api-with-azure-ad-authentication"></a>Hello d’accès API Azure Media Services avec l’authentification Azure AD
 
Hello API Azure Media Services est une API RESTful. Vous pouvez l’utiliser tooperform des opérations sur les ressources de support à l’aide d’une API REST ou à l’aide de kits de développement logiciel client disponible. Azure Media Services propose un Kit de développement logiciel (SDK) client Media Services pour Microsoft .NET. toobe autorisé des ressources de Media Services tooaccess et hello API Media Services, vous devez tout d’abord être authentifié. 

Media Services prend en charge l’[authentification avec Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md). Hello service REST de média Azure requiert que soit hello utilisateur de hello ou une application qui effectue des demandes d’API REST hello **collaborateur** ou **propriétaire** rôle tooaccess hello des ressources. Pour plus d’informations, consultez [prise en main le contrôle d’accès en fonction du rôle Bonjour Azure portal](../active-directory/role-based-access-control-what-is.md).  

> [!IMPORTANT]
> Actuellement, Media Services prend en charge le modèle d’authentification hello Azure Access Control service. Toutefois, l’autorisation Access Control sera déconseillée à compter du 1er juin 2018. Nous vous recommandons de migrer modèle d’authentification Azure AD de toohello dès que possible.

Ce document donne une vue d’ensemble de la façon dont tooaccess hello API Media Services à l’aide des API REST ou .NET.

## <a name="access-control"></a>Contrôle d’accès

Pour toosucceed de demande REST de Media Azure hello, utilisateur appelant de hello doit avoir un rôle de contributeur ou de propriétaire pour hello compte Media Services est la tentative de tooaccess.  
Seul un utilisateur avec le rôle de propriétaire hello peut donner media (compte) accès toonew les utilisateurs de ressources ou d’applications. rôle de collaborateur Hello accessible uniquement les ressources de support hello.
Les requêtes non autorisées échouent et génèrent le code d’état 401. Si vous voyez ce code d’erreur, vérifiez si l’utilisateur a hello contributeur ou rôle de propriétaire affecté hello compte d’utilisateur Media Services. Vous pouvez le vérifier dans hello portail Azure. Recherchez votre compte de média, puis cliquez sur hello **le contrôle d’accès** onglet. 

![Onglet Contrôle d’accès](./media/media-services-use-aad-auth-to-access-ams-api/media-services-access-control.png)

## <a name="types-of-authentication"></a>Types d’authentification 
 
Lorsque vous utilisez l’authentification Azure AD avec Azure Media Services, vous disposez de deux options d’authentification :

- **Authentification utilisateur**. Authentifier un utilisateur de hello application toointeract avec les ressources de Media Services. application interactive Hello doit tout d’abord utilisateur hello pour les informations d’identification de l’utilisateur hello. Un exemple est une application de console de gestion utilisée par les tâches d’encodage toomonitor des utilisateurs autorisés ou la diffusion en continu. 
- **Authentification d’un principal de service**. Authentifiez un service. Les applications qui utilisent généralement cette méthode d’authentification sont des applications qui exécutent des services démon, des services de niveau intermédiaire ou des travaux planifiés, par exemple les applications web, les applications de fonction, les applications logiques, les API ou les microservices.

### <a name="user-authentication"></a>Authentification utilisateur 

Les applications qui doivent utiliser de méthode d’authentification utilisateur hello sont gestion ou surveillance des applications natives : les applications mobiles, les applications Windows et les applications de Console. Ce type de solution est utile lorsque vous souhaitez que d’interaction humaine avec un service hello dans un des hello les scénarios suivants :

- Tableau de bord de surveillance pour vos travaux d’encodage.
- Tableau de bord de surveillance pour vos flux en direct.
- Application de gestion des ressources de tooadminister les utilisateurs de bureau ou portable dans un compte Media Services.

> [!NOTE]
> Cette méthode d’authentification ne doit pas être utilisée pour les applications accessibles aux consommateurs. 

Une application native doit d’abord acquérir un jeton d’accès d’Azure AD et ensuite l’utiliser lorsque vous apportez des API REST de HTTP demandes toohello Media Services. Ajouter un en-tête de demande de jeton toohello accès hello. 

Hello suivant schéma montre un flux d’authentification classique application interactive : 

![Diagramme d’applications natives](./media/media-services-use-aad-auth-to-access-ams-api/media-services-native-aad-app1.png)

Bonjour précédant le diagramme, hello nombres représentent des flux de hello de demandes hello dans l’ordre chronologique.

> [!NOTE]
> Lorsque vous utilisez la méthode d’authentification utilisateur hello, toutes les applications partagent hello même ID de client d’application native (par défaut) et l’application native URI de redirection. 

1. Demandez à un utilisateur ses informations d’identification.
2. Demander un jeton d’accès Azure AD avec hello paramètres suivants :  

    * Point de terminaison de locataire Azure AD.

        les informations du locataire Hello peuvent être récupérées de hello portail Azure. Placez votre curseur sur le nom de hello de hello utilisateur connecté dans le coin supérieur droit de hello.
    * URI de ressource Media Services. 

        Cet URI est hello même pour les comptes Media Services qui se trouvent dans hello même environnement Azure (par exemple, https://rest.media.azure.net).

    * ID client d’application Media Services (natif).
    * URI de redirection d’application Media Services (natif).
    * URI de ressource pour REST Media Services.
        
        Hello URI représente le point de terminaison API REST hello (par exemple, https://test03.restv2.westus.media.azure.net/api/).

    tooget des valeurs pour ces paramètres, consultez [utiliser les paramètres d’authentification tooaccess portail Azure AD Azure hello](media-services-portal-get-started-with-aad.md) à l’aide d’option d’authentification utilisateur hello.

3. jeton d’accès Azure AD de Hello est envoyée toohello client.
4. Hello en envoyant une demande de toohello API REST de Azure Media avec un jeton d’accès hello Azure AD.
5. client de Hello récupère les données de salutation de Media Services.

Pour plus d’informations sur comment toocommunicate d’authentification toouse Azure AD avec REST demande à l’aide de hello Media Services .NET client SDK, consultez [utilisent Azure AD authentication tooaccess hello API Media Services avec .NET](media-services-dotnet-get-started-with-aad.md). 

Si vous n’utilisez pas de client de Media Services .NET hello SDK, vous devez créer manuellement une demande de jeton d’accès Azure AD à l’aide de paramètres hello décrites à l’étape 2. Pour plus d’informations, consultez [comment toouse hello Azure AD Authentication Library tooget hello jeton Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

### <a name="service-principal-authentication"></a>Authentification d’un principal du service

Les applications qui utilisent généralement cette méthode d’authentification sont des applications qui exécutent des services de niveau intermédiaire et des travaux planifiés : applications web, applications de fonction, applications logiques, API et microservices. Cette méthode d’authentification est également adaptée aux applications interactives dans laquelle vous souhaiterez toouse un compte de service toomanage ressources.

Lorsque vous utilisez des scénarios de consommateur hello service authentification principale méthode toobuild, l’authentification est généralement gérée dans la couche intermédiaire de hello (via une API) et non directement dans une application mobile ou de bureau. 

toouse cette méthode, créez une application Azure AD et service principal dans son propre locataire. Après avoir créé des application hello, donnez à hello application contributeur ou propriétaire du rôle accès toohello compte Media Services. Vous pouvez cela Bonjour portail Azure, à l’aide de CLI d’Azure, ou avec un script PowerShell. Vous pouvez aussi utiliser une application Azure AD existante. Vous pouvez inscrire et gérer votre application Azure AD et votre service principal [Bonjour Azure portal](media-services-portal-get-started-with-aad.md). Vous pouvez également le faire à l’aide d’[Azure CLI 2.0](media-services-use-aad-auth-to-access-ams-api.md) ou de [PowerShell](media-services-powershell-create-and-configure-aad-app.md). 

![Applications de niveau intermédiaire](./media/media-services-use-aad-auth-to-access-ams-api/media-services-principal-service-aad-app1.png)

Après avoir créé votre application Azure AD, vous obtenez les valeurs pour hello suivant les paramètres. Vous avez besoin de ces valeurs pour l’authentification :

- ID client 
- Clé secrète client 

Bonjour précédant figure, hello nombres représentent des flux de hello de demandes hello dans l’ordre chronologique :
    
1. Une application de couche intermédiaire (API web ou une application web) demande un jeton d’accès Azure AD qui a hello paramètres suivants :  

    * Point de terminaison de locataire Azure AD.

        les informations du locataire Hello peuvent être récupérées de hello portail Azure. Placez votre curseur sur le nom de hello de hello utilisateur connecté dans le coin supérieur droit de hello.
    * URI de ressource Media Services. 

        Cet URI est hello même pour les comptes Media Services qui sont trouvent dans hello même environnement Azure (par exemple, https://rest.media.azure.net).

    * URI de ressource pour REST Media Services.

        Hello URI représente le point de terminaison API REST hello (par exemple, https://test03.restv2.westus.media.azure.net/api/).

    * Valeurs de l’application Azure AD : hello ID client et question secrète du client.
    
    tooget des valeurs pour ces paramètres, consultez [utiliser les paramètres d’authentification tooaccess portail Azure AD Azure hello](media-services-portal-get-started-with-aad.md) en utilisant l’option de l’authentification du principal de service hello.

2. jeton d’accès Azure AD de Hello est envoyée intermédiaire toohello.
4. niveau intermédiaire de Hello envoie la demande toohello API REST de Media Azure avec un jeton d’Azure AD hello.
5. niveau intermédiaire de Hello récupère les données de salutation de Media Services.

Pour plus d’informations sur la façon dont toocommunicate d’authentification toouse Azure AD avec REST demande à l’aide de hello Media Services .NET client SDK, consultez [utilisent Azure AD authentication tooaccess API Azure Media Services avec .NET](media-services-dotnet-get-started-with-aad.md). 

Si vous n’utilisez pas de client de Media Services .NET hello SDK, vous devez créer manuellement une demande de jeton Azure AD à l’aide des paramètres décrits à l’étape 1. Pour plus d’informations, consultez [comment toouse hello Azure AD Authentication Library tooget hello jeton Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).

## <a name="troubleshooting"></a>Résolution des problèmes

Exception : « à distance hello a renvoyé une erreur : (401) non autorisé. »

Solution : Pour hello toosucceed de demande REST de Media Services, les utilisateur appelant hello doivent être un rôle de contributeur ou propriétaire Bonjour compte Media Services est la tentative de tooaccess. Pour plus d’informations, consultez hello [le contrôle d’accès](media-services-use-aad-auth-to-access-ams-api.md#access-control) section.

## <a name="resources"></a>Ressources

Hello suivant des articles des vues d’ensemble des concepts d’authentification Azure AD : 

- [Scénarios d’authentification pour Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md#basics-of-authentication-in-azure-ad)
- [Add, update, or remove an application in Azure AD](../active-directory/develop/active-directory-integrating-applications.md) (Ajouter, mettre à jour ou supprimer une application dans Azure AD)
- [Configure and manage Role-Based Access Control by using PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md) (Configurer et gérer le contrôle d’accès en fonction du rôle à l’aide de PowerShell)

## <a name="next-steps"></a>Étapes suivantes

* Utilisez hello portail Azure trop[tooconsume d’authentification Azure AD Azure Media Services API d’accès](media-services-portal-get-started-with-aad.md).
* Utiliser l’authentification Azure AD trop[accéder aux API Azure Media Services avec .NET](media-services-dotnet-get-started-with-aad.md).

