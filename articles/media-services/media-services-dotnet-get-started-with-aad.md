---
title: "aaaUse tooaccess d’authentification Azure AD API Azure Media Services avec .NET | Documents Microsoft"
description: "Cette rubrique montre comment toouse tooaccess d’authentification Azure Active Directory (Azure AD) Azure Media Services (AMS) des API avec .NET."
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
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a>Utiliser Azure AD authentication tooaccess API Azure Media Services avec .NET

À partir de windowsazure.mediaservices 4.0.0.4, Azure Media Services prend en charge l’authentification basée sur Azure Active Directory (Azure AD). Cette rubrique vous montre comment toouse tooaccess d’authentification Azure AD API Azure Media Services avec Microsoft .NET.

## <a name="prerequisites"></a>Composants requis

- Un compte Azure. Pour plus d’informations, consultez la page [Version d’évaluation gratuite d’Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Un compte Media Services. Pour plus d’informations, consultez [créer un compte Azure Media Services à l’aide de hello Azure portal](media-services-portal-create-account.md).
- Hello dernières [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.
- Connaissance de la rubrique de hello [l’accès à des API Azure Media Services avec une vue d’ensemble de l’authentification AAD](media-services-use-aad-auth-to-access-ams-api.md). 

Lorsque vous utilisez l’authentification Azure AD avec Azure Media Services, vous pouvez vous authentifier de deux manières :

- **Authentification utilisateur** authentifie un utilisateur de hello application toointeract avec des ressources Azure Media Services. les applications interactives Hello doivent tout d’abord utilisateur hello pour les informations d’identification. Un exemple est une application de console de gestion qui est utilisée par toomonitor les utilisateurs autorisés travaux d’encodage ou de diffusion en continu. 
- L’**authentification de principal de service** authentifie un service. Les applications qui utilisent généralement cette méthode d’authentification sont des applications qui exécutent des services démon, des services de niveau intermédiaire ou des travaux planifiés (par exemple, applications web, applications de fonction, applications logiques, API ou microservices).

>[!IMPORTANT]
>Azure Media Services prend actuellement en charge un modèle d’authentification Azure Access Control Service. Toutefois, l’autorisation de contrôle d’accès est en cours toobe déconseillée sur le 1 juin 2018. Nous vous recommandons de migrer modèle d’authentification Azure Active Directory tooan dès que possible.

## <a name="get-an-azure-ad-access-token"></a>Obtenir un jeton d’accès Azure AD

tooconnect toohello API Azure Media Services avec l’authentification Azure AD, application de client hello doit toorequest un jeton d’accès Azure AD. Lorsque vous utilisez le SDK, nombreux hello plus d’informations sur comment tooacquire un jeton d’accès Azure AD sont encapsulées et simplifiée pour vous dans hello du client de Media Services .NET hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) et [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes. 

Par exemple, vous n’avez pas besoin tooprovide hello Azure AD autorité, URI de ressource de Media Services ou natif détails de l’application Azure AD. Il s’agit des valeurs connues qui sont déjà configurés par hello classe de fournisseur de jetons d’accès Azure AD. 

Si vous n’utilisez pas d’Azure Media Services .NET SDK, nous vous recommandons d’utiliser hello [bibliothèque d’authentification Azure AD](../active-directory/develop/active-directory-authentication-libraries.md). les valeurs de tooget des paramètres de hello que vous avez besoin de toouse avec la bibliothèque d’authentification Azure AD, consultez [utiliser les paramètres d’authentification tooaccess portail Azure AD Azure hello](media-services-portal-get-started-with-aad.md).

Vous avez également option hello de remplacer l’implémentation par défaut de hello Hello **AzureAdTokenProvider** avec votre propre implémentation.

## <a name="install-and-configure-azure-media-services-net-sdk"></a>Installer et configurer le kit de développement logiciel (SDK) Azure Media Services pour .NET

>[!NOTE] 
>authentification toouse Azure AD avec hello Media Services .NET SDK, vous devez toohave hello dernières [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package. En outre, ajoutez une référence toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly. Si vous utilisez une application existante, inclure hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly. 

1. Créez une application console C# dans Visual Studio.
2. Hello d’utilisation [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall de package NuGet **Azure Media Services .NET SDK**. 

    tooadd des références à l’aide de NuGet, prendre hello comme suit : dans **l’Explorateur de solutions**, cliquez sur le nom de projet hello, puis sélectionnez **gérer les packages NuGet**. Ensuite, recherchez **windowsazure.mediaservices** et cliquez sur **Installer**.
    
    -ou-

    Exécution hello après une commande dans **Package Manager Console** dans Visual Studio.

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. Ajouter **à l’aide de** code source de tooyour.

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a>Utiliser une authentification utilisateur

tooconnect toohello API de Service de média Azure avec l’option d’authentification utilisateur hello, hello client application doit toorequest hello d’un jeton d’Azure AD à l’aide de paramètres suivants :  

- Point de terminaison de locataire Azure AD. les informations du locataire Hello peuvent être récupérées de hello portail Azure. Pointez sur hello utilisateur connecté dans le coin supérieur droit de hello.
- URI de ressource Media Services.
- ID client d’application Media Services (natif). 
- URI de redirection d’application Media Services (natif). 

les valeurs Hello pour ces paramètres sont accessibles dans **AzureEnvironments.AzureCloudEnvironment**. Hello **AzureEnvironments.AzureCloudEnvironment** constante est une application d’assistance dans hello .NET SDK tooget hello droit variable paramètres d’environnement pour un centre de données Azure publique. 

Il contient des paramètres d’environnement prédéfinis pour accéder aux Services de support dans des centres de données publics hello uniquement. Pour les régions de cloud souverain ou gouvernemental, vous pouvez utiliser **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment** ou **AzureGermanCloudEnvironment** respectivement.

Hello, exemple de code suivant crée un jeton :
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
toostart programmation de Media Services, vous devez toocreate une **CloudMediaContext** instance qui représente le contexte de serveur hello. Hello **CloudMediaContext** contient des collections de tooimportant de références, y compris les travaux actifs, fichiers, les stratégies d’accès et les localisateurs. 

Vous devez également toopass hello **ressource URI des Services REST de Media** toohello **CloudMediaContext** constructeur. URI de la ressource tooget hello pour les Services REST de Media, connectez-vous toohello portail Azure, sélectionnez votre compte Azure Media Services, sélectionnez **l’accès aux API**, puis sélectionnez **connecter tooAzure Media Services avec l’utilisateur authentification**. 

Hello exemple de code suivant crée un **CloudMediaContext** instance :

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

Bonjour à l’exemple suivant montre comment toocreate hello contexte de jeton et hello Azure AD :

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
>Si vous obtenez une exception indiquant que « serveur hello a renvoyé une erreur : non autorisé de (401), « voir hello [le contrôle d’accès](media-services-use-aad-auth-to-access-ams-api.md#access-control) section de l’accès à des API Azure Media Services, vue d’ensemble de l’authentification Azure AD.

## <a name="use-service-principal-authentication"></a>Utiliser une authentification de principal de service
    
tooconnect toohello API Azure Media Services avec l’option principal du service hello, votre application de couche intermédiaire (API web ou une application web) doit toorequests un jeton Azure AD avec hello paramètres suivants :  

- Point de terminaison de locataire Azure AD. les informations du locataire Hello peuvent être récupérées de hello portail Azure. Pointez sur hello utilisateur connecté dans le coin supérieur droit de hello.
- URI de ressource Media Services.
- Valeurs de l’application Azure AD : hello **ID Client** et **clé secrète Client**.

Hello des valeurs pour hello **ID Client** et **clé secrète Client** paramètres peuvent être trouvés dans hello portail Azure. Pour plus d’informations, consultez [prise en main d’Azure AD à l’aide de l’authentification hello Azure portal](media-services-portal-get-started-with-aad.md).

Hello exemple de code suivant crée un jeton à l’aide de hello **AzureAdTokenCredentials** constructeur qui accepte **AzureAdClientSymmetricKey** en tant que paramètre : 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

Vous pouvez également spécifier hello **AzureAdTokenCredentials** constructeur qui accepte **AzureAdClientCertificate** en tant que paramètre. 

Pour obtenir des instructions sur la façon toocreate et configurer un certificat dans un formulaire qui peut être utilisé par Azure AD, consultez [authentification tooAzure AD dans les applications avec des certificats - étapes de configuration manuelles démon](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

toostart programmation de Media Services, vous devez toocreate une **CloudMediaContext** instance qui représente le contexte de serveur hello. Vous devez également toopass hello **ressource URI des Services REST de Media** toohello **CloudMediaContext** constructeur. Vous pouvez obtenir hello **ressource URI des Services REST de Media** comprise hello également le portail Azure.

Hello exemple de code suivant crée un **CloudMediaContext** instance :

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
Bonjour à l’exemple suivant montre comment toocreate hello contexte de jeton et hello Azure AD :

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a>Étapes suivantes

Prise en main [téléchargement de fichiers tooyour compte](media-services-dotnet-upload-files.md).
