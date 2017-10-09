---
title: "Compte de Services de tooMedia aaaConnecting à l’aide de .NET"
description: Cette rubrique montre comment utiliser les Services de tooMedia tooconnect .NET.
services: media-services
documentationcenter: 
author: juliako
manager: erikre
editor: 
ms.assetid: a8412a29-59dc-44a0-ace0-be79a97dab63
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/26/2016
ms.author: juliako
ms.openlocfilehash: a23bd285f7cae17ae5831e1e50e73947afbb9a3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a>Connexion tooMedia compte de Services à l’aide de Media Services SDK pour .NET
> [!div class="op_single_selector"]
> * [REST](media-services-rest-connect-programmatically.md)
> * [.NET](media-services-dotnet-connect-programmatically.md)
> 
> 

Cette rubrique décrit comment tooobtain un tooMicrosoft de connexion par programmation Azure Media Services lorsque vous programmez avec hello Media Services SDK pour .NET.

## <a name="connecting-toomedia-services"></a>Connecter les Services tooMedia
tooconnect tooMedia Services par programme, vous devez disposer précédemment configuré un compte Azure, configuré les Services de support sur ce compte et ensuite définir un projet Visual Studio pour le développement avec hello Media Services SDK pour .NET. Pour plus d’informations, consultez le programme d’installation pour le développement avec hello Media Services SDK pour .NET.

Extrémité hello du processus de configuration de compte Media Services hello, vous avez obtenu suivantes hello valeurs de connexion. Utiliser ces connexions par programme toomake tooMedia Services.

* Le nom de votre compte Media Services.
* Votre clé de compte Media Services.

toofind ces valeurs, accédez toohello portail de gestion Azure, sélectionnez votre compte de Service de support et cliquez sur hello »**gérer les clés**« icône bas hello de fenêtre du portail hello. En cliquant sur hello icône suivant tooeach texte boîte copies hello valeur toohello Presse-papiers du système.

## <a name="creating-a-cloudmediacontext-instance"></a>Création d’une instance CloudMediaContext
toostart programmation Media Services, vous devez toocreate une **CloudMediaContext** instance qui représente le contexte de serveur hello. Hello **CloudMediaContext** contient des collections de tooimportant de références, y compris les travaux actifs, fichiers, les stratégies d’accès et les localisateurs.

> [!NOTE]
> Hello **CloudMediaContext** classe n’est pas thread-safe. Vous devez créer un nouveau CloudMediaContext par thread ou par ensemble d’opérations.
> 
> 

CloudMediaContext a cinq surcharges de constructeur. Il est recommandé toouse des constructeurs qui acceptent **MediaServicesCredentials** en tant que paramètre. Pour plus d’informations, consultez hello **réutilisation des jetons du Service de contrôle accès** qui suit. 

Hello exemple suivant utilise hello publique CloudMediaContext(MediaServicesCredentials credentials) constructeur :

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a>Réutilisation des jetons Access Control Service
Cette section montre comment les jetons de tooreuse Service de contrôle d’accès à l’aide de constructeurs CloudMediaContext prenant MediaServicesCredentials en tant que paramètre.

[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (également appelé Access Control Service ou ACS) est un service cloud qui fournit un moyen facile d’authentification et d’autorisation aux utilisateurs d’accéder toogain tootheir des applications web. Microsoft Azure Media Services contrôle l’accès tooits services cependant protocole OAuth qui nécessite un jeton ACS. Media Services reçoit les jetons ACS hello à partir d’un serveur d’autorisation.

Lorsque vous développez avec hello Media Services SDK, vous pouvez choisir toonot traitent les jetons hello car hello gestionnaires de code SDK pour vous. Toutefois, vous permettant de hello SDK gérer entièrement hello ACS jetons prospects toounnecessary les demandes de jeton. Demande de jetons prend du temps et consomme les ressources client et serveur hello. En outre, serveur d’ACS hello limite les demandes hello si hello taux est trop élevé. limite de Hello est de 30 demandes par seconde, consultez [Limitations du Service ACS](https://msdn.microsoft.com/library/gg185909.aspx) pour plus d’informations.

À compter de hello SDK Media Services version 3.0.0.0, vous pouvez réutiliser les jetons ACS hello. Hello **CloudMediaContext** constructeurs qui acceptent **MediaServicesCredentials** comme paramètre permettent le partage des jetons hello ACS entre plusieurs contextes. Hello MediaServicesCredentials classe encapsule des informations d’identification du service de média hello. Si un jeton ACS est disponible et son heure d’expiration est connue, vous pouvez créer une nouvelle instance de MediaServicesCredentials avec un jeton de hello et passez-le constructeur toohello de CloudMediaContext. Notez que Media Services SDK hello actualise automatiquement les jetons quand ils expirent. Voici deux façons tooreuse les jetons ACS, comme indiqué dans les exemples hello ci-dessous.

* Vous pouvez mettre en cache hello **MediaServicesCredentials** objet en mémoire (par exemple, dans une variable de classe statique). Ensuite, transmettez le constructeur de CloudMediaContext toohello l’objet hello mis en cache. objet de Hello MediaServicesCredentials contient un jeton ACS qui peut être réutilisé s’il est toujours valide. Si le jeton de hello n’est pas valide, qu'il est réactualisé par hello Media Services SDK à l’aide des informations d’identification hello donné toohello MediaServicesCredentials constructeur.
  
    Notez que hello **MediaServicesCredentials** objet Obtient un jeton valide après hello RefreshToken est appelée. Hello **CloudMediaContext** hello d’appels **RefreshToken** méthode dans le constructeur de hello. Si vous envisagez de stockage de tooan de valeurs de jeton hello toosave externe, prendre toocheck que hello TokenExpiration valeur n’est valide avant d’enregistrer les données du jeton hello. S’il n’est pas valide, appelez RefreshToken avant la mise en cache.
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* Vous pouvez également mettre en cache hello AccessToken valeurs de chaîne et hello TokenExpiration. les valeurs Hello peut être ultérieurement utilisé toocreate un nouveau MediaServicesCredentials de l’objet avec les données de jeton hello mis en cache.  Cela est particulièrement utile pour les scénarios où le jeton de hello peut être partagé en toute sécurité entre plusieurs processus ou ordinateurs.
  
    Hello extraits de code suivants appellent hello méthodes SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage et UpdateTokenDataInExternalStorageIfNeeded qui ne sont pas définis dans cet exemple. Vous pouvez définir ces méthodes toostore, la récupération et la mise à jour les données de jeton dans un stockage externe. 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    Utilisez hello enregistré les valeurs de jeton toocreate MediaServicesCredentials.

        var accessToken = "";
        var tokenExpiration = DateTime.UtcNow;

        // Retrieve saved token values.
        GetTokenDataFromExternalStorage(out accessToken, out tokenExpiration);

        // Create a new MediaServicesCredentials object using saved token values.
        MediaServicesCredentials credentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey)
        {
            AccessToken = accessToken,
            TokenExpiration = tokenExpiration
        };

        CloudMediaContext context2 = new CloudMediaContext(credentials);

    Mettre à jour de copie du jeton hello en cas de mise à jour de jeton de hello en hello Media Services SDK. 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* Si vous avez plusieurs comptes Media Services (par exemple, pour le partage de charge à des fins ou distribution géographique) vous pouvez mettre en cache les objets MediaServicesCredentials à l’aide de la collection de System.Collections.Concurrent.ConcurrentDictionary hello (hello Collection de ConcurrentDictionary représente une collection thread-safe de paires clé/valeur accessibles par plusieurs threads simultanément). Vous pouvez ensuite utiliser les informations d’identification de hello GetOrAdd méthode tooget hello mis en cache. 
  
        // Declare a static class variable of hello ConcurrentDictionary type in which hello Media Services credentials will be cached.  
        private static readonly ConcurrentDictionary<string, MediaServicesCredentials> mediaServicesCredentialsCache = 
            new ConcurrentDictionary<string, MediaServicesCredentials>();

        // Cache (or get already cached) Media Services credentials. Use these credentials toocreate a new CloudMediaContext object.
        static public CloudMediaContext CreateMediaServicesContext(string accountName, string accountKey)
        {
            CloudMediaContext cloudMediaContext;
            MediaServicesCredentials mediaServicesCredentials;

            mediaServicesCredentials = mediaServicesCredentialsCache.GetOrAdd(
                accountName,
                valueFactory => new MediaServicesCredentials(accountName, accountKey));

            cloudMediaContext = new CloudMediaContext(mediaServicesCredentials);

            return cloudMediaContext;
        }

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a>Connexion de compte de service de média tooa situé dans une région hello en Chine du Nord
Si votre compte se trouve dans la région de hello en Chine du Nord, utilisez hello suivant constructeur :

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

Par exemple :

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a>Stockage des valeurs de connexion dans la configuration
Il s’agit d’une valeur de connexion hautement recommandé toostore, notamment les valeurs sensibles telles que votre nom de compte et un mot de passe, dans la configuration. Il est également une données de configuration sensibles tooencrypt pratique recommandée. Vous pouvez chiffrer le fichier de configuration hello à l’aide de hello Windows EFS (ENCRYPTING file). tooenable EFS sur un fichier, avec le bouton hello, sélectionnez **propriétés**et activer le chiffrement Bonjour **avancé** onglet Paramètres. Vous pouvez également créer une solution personnalisée pour le chiffrement des parties sélectionnées d’un fichier de configuration à l’aide de la configuration protégée. Consultez la page [Chiffrement des informations de configuration à l'aide de la configuration protégée](https://msdn.microsoft.com/library/53tyfkaw.aspx).

Hello, le fichier App.config suivant contient des valeurs de connexion hello requis. Hello valeurs Bonjour <appSettings> élément sont les valeurs hello requises que vous avez obtenu à partir du processus d’installation de hello Media Services compte.

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


tooretrieve les valeurs de connexion de configuration, vous pouvez utiliser hello **ConfigurationManager** classe, puis affectez toofields de valeurs hello dans votre code :

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

