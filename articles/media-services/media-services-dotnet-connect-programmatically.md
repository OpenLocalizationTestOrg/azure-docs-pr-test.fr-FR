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
# <a name="connecting-toomedia-services-account-using-media-services-sdk-for-net"></a><span data-ttu-id="48f70-103">Connexion tooMedia compte de Services à l’aide de Media Services SDK pour .NET</span><span class="sxs-lookup"><span data-stu-id="48f70-103">Connecting tooMedia Services Account using Media Services SDK for .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="48f70-104">REST</span><span class="sxs-lookup"><span data-stu-id="48f70-104">REST</span></span>](media-services-rest-connect-programmatically.md)
> * [<span data-ttu-id="48f70-105">.NET</span><span class="sxs-lookup"><span data-stu-id="48f70-105">.NET</span></span>](media-services-dotnet-connect-programmatically.md)
> 
> 

<span data-ttu-id="48f70-106">Cette rubrique décrit comment tooobtain un tooMicrosoft de connexion par programmation Azure Media Services lorsque vous programmez avec hello Media Services SDK pour .NET.</span><span class="sxs-lookup"><span data-stu-id="48f70-106">This topic describes how tooobtain a programmatic connection tooMicrosoft Azure Media Services when you are programming with hello Media Services SDK for .NET.</span></span>

## <a name="connecting-toomedia-services"></a><span data-ttu-id="48f70-107">Connecter les Services tooMedia</span><span class="sxs-lookup"><span data-stu-id="48f70-107">Connecting tooMedia Services</span></span>
<span data-ttu-id="48f70-108">tooconnect tooMedia Services par programme, vous devez disposer précédemment configuré un compte Azure, configuré les Services de support sur ce compte et ensuite définir un projet Visual Studio pour le développement avec hello Media Services SDK pour .NET.</span><span class="sxs-lookup"><span data-stu-id="48f70-108">tooconnect tooMedia Services programmatically, you must have previously set up an Azure account, configured Media Services on that account, and then set up a Visual Studio project for development with hello Media Services SDK for .NET.</span></span> <span data-ttu-id="48f70-109">Pour plus d’informations, consultez le programme d’installation pour le développement avec hello Media Services SDK pour .NET.</span><span class="sxs-lookup"><span data-stu-id="48f70-109">For more information, see Setup for Development with hello Media Services SDK for .NET.</span></span>

<span data-ttu-id="48f70-110">Extrémité hello du processus de configuration de compte Media Services hello, vous avez obtenu suivantes hello valeurs de connexion.</span><span class="sxs-lookup"><span data-stu-id="48f70-110">At hello end of hello Media Services account setup process, you obtained hello following required connection values.</span></span> <span data-ttu-id="48f70-111">Utiliser ces connexions par programme toomake tooMedia Services.</span><span class="sxs-lookup"><span data-stu-id="48f70-111">Use these toomake programmatic connections tooMedia Services.</span></span>

* <span data-ttu-id="48f70-112">Le nom de votre compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="48f70-112">Your Media Services account name.</span></span>
* <span data-ttu-id="48f70-113">Votre clé de compte Media Services.</span><span class="sxs-lookup"><span data-stu-id="48f70-113">Your Media Services account key.</span></span>

<span data-ttu-id="48f70-114">toofind ces valeurs, accédez toohello portail de gestion Azure, sélectionnez votre compte de Service de support et cliquez sur hello »**gérer les clés**« icône bas hello de fenêtre du portail hello.</span><span class="sxs-lookup"><span data-stu-id="48f70-114">toofind these values, go toohello Azure Managment Portal, select your Media Service account, and click on hello “**MANAGE KEYS**” icon on hello bottom of hello portal window.</span></span> <span data-ttu-id="48f70-115">En cliquant sur hello icône suivant tooeach texte boîte copies hello valeur toohello Presse-papiers du système.</span><span class="sxs-lookup"><span data-stu-id="48f70-115">Clicking on hello icon next tooeach text box copies hello value toohello system clipboard.</span></span>

## <a name="creating-a-cloudmediacontext-instance"></a><span data-ttu-id="48f70-116">Création d’une instance CloudMediaContext</span><span class="sxs-lookup"><span data-stu-id="48f70-116">Creating a CloudMediaContext Instance</span></span>
<span data-ttu-id="48f70-117">toostart programmation Media Services, vous devez toocreate une **CloudMediaContext** instance qui représente le contexte de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="48f70-117">toostart programming against Media Services you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="48f70-118">Hello **CloudMediaContext** contient des collections de tooimportant de références, y compris les travaux actifs, fichiers, les stratégies d’accès et les localisateurs.</span><span class="sxs-lookup"><span data-stu-id="48f70-118">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span>

> [!NOTE]
> <span data-ttu-id="48f70-119">Hello **CloudMediaContext** classe n’est pas thread-safe.</span><span class="sxs-lookup"><span data-stu-id="48f70-119">hello **CloudMediaContext** class is not thread safe.</span></span> <span data-ttu-id="48f70-120">Vous devez créer un nouveau CloudMediaContext par thread ou par ensemble d’opérations.</span><span class="sxs-lookup"><span data-stu-id="48f70-120">You should create a new CloudMediaContext per thread or per set of operations.</span></span>
> 
> 

<span data-ttu-id="48f70-121">CloudMediaContext a cinq surcharges de constructeur.</span><span class="sxs-lookup"><span data-stu-id="48f70-121">CloudMediaContext has five constructor overloads.</span></span> <span data-ttu-id="48f70-122">Il est recommandé toouse des constructeurs qui acceptent **MediaServicesCredentials** en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="48f70-122">It is recommended toouse constructors that take **MediaServicesCredentials** as a parameter.</span></span> <span data-ttu-id="48f70-123">Pour plus d’informations, consultez hello **réutilisation des jetons du Service de contrôle accès** qui suit.</span><span class="sxs-lookup"><span data-stu-id="48f70-123">For more information, see hello **Reusing Access Control Service Tokens** that follows.</span></span> 

<span data-ttu-id="48f70-124">Hello exemple suivant utilise hello publique CloudMediaContext(MediaServicesCredentials credentials) constructeur :</span><span class="sxs-lookup"><span data-stu-id="48f70-124">hello following example uses hello public CloudMediaContext(MediaServicesCredentials credentials) constructor:</span></span>

    // _cachedCredentials and _context are class member variables. 
    _cachedCredentials = new MediaServicesCredentials(
                    _mediaServicesAccountName,
                    _mediaServicesAccountKey);

    _context = new CloudMediaContext(_cachedCredentials);


## <a name="reusing-access-control-service-tokens"></a><span data-ttu-id="48f70-125">Réutilisation des jetons Access Control Service</span><span class="sxs-lookup"><span data-stu-id="48f70-125">Reusing Access Control Service Tokens</span></span>
<span data-ttu-id="48f70-126">Cette section montre comment les jetons de tooreuse Service de contrôle d’accès à l’aide de constructeurs CloudMediaContext prenant MediaServicesCredentials en tant que paramètre.</span><span class="sxs-lookup"><span data-stu-id="48f70-126">This section shows how tooreuse Access Control Service tokens by using CloudMediaContext constructors that take MediaServicesCredentials as a parameter.</span></span>

<span data-ttu-id="48f70-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (également appelé Access Control Service ou ACS) est un service cloud qui fournit un moyen facile d’authentification et d’autorisation aux utilisateurs d’accéder toogain tootheir des applications web.</span><span class="sxs-lookup"><span data-stu-id="48f70-127">[Azure Active Directory Access Control](https://msdn.microsoft.com/library/hh147631.aspx) (also known as Access Control Service or ACS) is a cloud-based service that provides an easy way of authenticating and authorizing users toogain access tootheir web applications.</span></span> <span data-ttu-id="48f70-128">Microsoft Azure Media Services contrôle l’accès tooits services cependant protocole OAuth qui nécessite un jeton ACS.</span><span class="sxs-lookup"><span data-stu-id="48f70-128">Microsoft Azure Media Services controls access tooits services though OAuth protocol that requires an ACS token.</span></span> <span data-ttu-id="48f70-129">Media Services reçoit les jetons ACS hello à partir d’un serveur d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="48f70-129">Media Services receives hello ACS tokens from an authorization server.</span></span>

<span data-ttu-id="48f70-130">Lorsque vous développez avec hello Media Services SDK, vous pouvez choisir toonot traitent les jetons hello car hello gestionnaires de code SDK pour vous.</span><span class="sxs-lookup"><span data-stu-id="48f70-130">When developing with hello Media Services SDK, you can choose toonot deal with hello tokens because hello SDK code managers them for you.</span></span> <span data-ttu-id="48f70-131">Toutefois, vous permettant de hello SDK gérer entièrement hello ACS jetons prospects toounnecessary les demandes de jeton.</span><span class="sxs-lookup"><span data-stu-id="48f70-131">However, letting hello SDK fully manage hello ACS tokens leads toounnecessary token requests.</span></span> <span data-ttu-id="48f70-132">Demande de jetons prend du temps et consomme les ressources client et serveur hello.</span><span class="sxs-lookup"><span data-stu-id="48f70-132">Requesting tokens takes time and consumes hello client and server resources.</span></span> <span data-ttu-id="48f70-133">En outre, serveur d’ACS hello limite les demandes hello si hello taux est trop élevé.</span><span class="sxs-lookup"><span data-stu-id="48f70-133">Also, hello ACS server throttles hello requests if hello rate is too high.</span></span> <span data-ttu-id="48f70-134">limite de Hello est de 30 demandes par seconde, consultez [Limitations du Service ACS](https://msdn.microsoft.com/library/gg185909.aspx) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="48f70-134">hello limit is 30 requests per second, see [ACS Service Limitations](https://msdn.microsoft.com/library/gg185909.aspx) for more details.</span></span>

<span data-ttu-id="48f70-135">À compter de hello SDK Media Services version 3.0.0.0, vous pouvez réutiliser les jetons ACS hello.</span><span class="sxs-lookup"><span data-stu-id="48f70-135">Starting with hello Media Services SDK version 3.0.0.0, you can reuse hello ACS tokens.</span></span> <span data-ttu-id="48f70-136">Hello **CloudMediaContext** constructeurs qui acceptent **MediaServicesCredentials** comme paramètre permettent le partage des jetons hello ACS entre plusieurs contextes.</span><span class="sxs-lookup"><span data-stu-id="48f70-136">hello **CloudMediaContext** constructors that take **MediaServicesCredentials** as a parameter enable sharing hello ACS tokens between multiple contexts.</span></span> <span data-ttu-id="48f70-137">Hello MediaServicesCredentials classe encapsule des informations d’identification du service de média hello.</span><span class="sxs-lookup"><span data-stu-id="48f70-137">hello MediaServicesCredentials class encapsulates hello Media Services credentials.</span></span> <span data-ttu-id="48f70-138">Si un jeton ACS est disponible et son heure d’expiration est connue, vous pouvez créer une nouvelle instance de MediaServicesCredentials avec un jeton de hello et passez-le constructeur toohello de CloudMediaContext.</span><span class="sxs-lookup"><span data-stu-id="48f70-138">If an ACS token is available and its expiration time is known, you can create a new MediaServicesCredentials instance with hello token and pass it toohello constructor of CloudMediaContext.</span></span> <span data-ttu-id="48f70-139">Notez que Media Services SDK hello actualise automatiquement les jetons quand ils expirent.</span><span class="sxs-lookup"><span data-stu-id="48f70-139">Note that hello Media Services SDK automatically refreshes tokens whenever they expire.</span></span> <span data-ttu-id="48f70-140">Voici deux façons tooreuse les jetons ACS, comme indiqué dans les exemples hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="48f70-140">There are two ways tooreuse ACS tokens, as shown in hello examples below.</span></span>

* <span data-ttu-id="48f70-141">Vous pouvez mettre en cache hello **MediaServicesCredentials** objet en mémoire (par exemple, dans une variable de classe statique).</span><span class="sxs-lookup"><span data-stu-id="48f70-141">You can cache hello **MediaServicesCredentials** object in memory (for example, in a static class variable).</span></span> <span data-ttu-id="48f70-142">Ensuite, transmettez le constructeur de CloudMediaContext toohello l’objet hello mis en cache.</span><span class="sxs-lookup"><span data-stu-id="48f70-142">Then, pass hello cached object toohello CloudMediaContext constructor.</span></span> <span data-ttu-id="48f70-143">objet de Hello MediaServicesCredentials contient un jeton ACS qui peut être réutilisé s’il est toujours valide.</span><span class="sxs-lookup"><span data-stu-id="48f70-143">hello MediaServicesCredentials object contains an ACS token that can be reused if it is still valid.</span></span> <span data-ttu-id="48f70-144">Si le jeton de hello n’est pas valide, qu'il est réactualisé par hello Media Services SDK à l’aide des informations d’identification hello donné toohello MediaServicesCredentials constructeur.</span><span class="sxs-lookup"><span data-stu-id="48f70-144">If hello token is not valid, it will be refreshed by hello Media Services SDK using hello credentials given toohello MediaServicesCredentials constructor.</span></span>
  
    <span data-ttu-id="48f70-145">Notez que hello **MediaServicesCredentials** objet Obtient un jeton valide après hello RefreshToken est appelée.</span><span class="sxs-lookup"><span data-stu-id="48f70-145">Note that hello **MediaServicesCredentials** object gets a valid token after hello RefreshToken is called.</span></span> <span data-ttu-id="48f70-146">Hello **CloudMediaContext** hello d’appels **RefreshToken** méthode dans le constructeur de hello.</span><span class="sxs-lookup"><span data-stu-id="48f70-146">hello **CloudMediaContext** calls hello **RefreshToken** method in hello constructor.</span></span> <span data-ttu-id="48f70-147">Si vous envisagez de stockage de tooan de valeurs de jeton hello toosave externe, prendre toocheck que hello TokenExpiration valeur n’est valide avant d’enregistrer les données du jeton hello.</span><span class="sxs-lookup"><span data-stu-id="48f70-147">If you are planning toosave hello token values tooan external storage, make sure toocheck whether hello TokenExpiration value is valid before saving hello token data.</span></span> <span data-ttu-id="48f70-148">S’il n’est pas valide, appelez RefreshToken avant la mise en cache.</span><span class="sxs-lookup"><span data-stu-id="48f70-148">If it is not valid, call RefreshToken before caching.</span></span>
  
        // Create and cache hello Media Services credentials in a static class variable.
        _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);

        // Use hello cached credentials toocreate a new CloudMediaContext object.
        if(_cachedCredentials == null)
        {
            _cachedCredentials = new MediaServicesCredentials(_mediaServicesAccountName, _mediaServicesAccountKey);
        }

        CloudMediaContext context = new CloudMediaContext(_cachedCredentials);

* <span data-ttu-id="48f70-149">Vous pouvez également mettre en cache hello AccessToken valeurs de chaîne et hello TokenExpiration.</span><span class="sxs-lookup"><span data-stu-id="48f70-149">You can also cache hello AccessToken string and hello TokenExpiration values.</span></span> <span data-ttu-id="48f70-150">les valeurs Hello peut être ultérieurement utilisé toocreate un nouveau MediaServicesCredentials de l’objet avec les données de jeton hello mis en cache.</span><span class="sxs-lookup"><span data-stu-id="48f70-150">hello values could later be used toocreate a new MediaServicesCredentials object with hello cached token data.</span></span>  <span data-ttu-id="48f70-151">Cela est particulièrement utile pour les scénarios où le jeton de hello peut être partagé en toute sécurité entre plusieurs processus ou ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="48f70-151">This is especially useful for scenarios where hello token can be securely shared among multiple processes or computers.</span></span>
  
    <span data-ttu-id="48f70-152">Hello extraits de code suivants appellent hello méthodes SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage et UpdateTokenDataInExternalStorageIfNeeded qui ne sont pas définis dans cet exemple.</span><span class="sxs-lookup"><span data-stu-id="48f70-152">hello following code snippets call hello SaveTokenDataToExternalStorage, GetTokenDataFromExternalStorage, and UpdateTokenDataInExternalStorageIfNeeded methods that are not defined in this example.</span></span> <span data-ttu-id="48f70-153">Vous pouvez définir ces méthodes toostore, la récupération et la mise à jour les données de jeton dans un stockage externe.</span><span class="sxs-lookup"><span data-stu-id="48f70-153">You could define these methods toostore, retrieve, and update token data in an external storage.</span></span> 
  
        CloudMediaContext context1 = new CloudMediaContext(_mediaServicesAccountName, _mediaServicesAccountKey);
  
        // Get token values from hello context.
        var accessToken = context1.Credentials.AccessToken;
        var tokenExpiration = context1.Credentials.TokenExpiration;
  
        // Save token values for later use. 
        // hello SaveTokenDataToExternalStorage method should check 
        // whether hello TokenExpiration value is valid before saving hello token data. 
        // If it is not valid, call MediaServicesCredentials’s RefreshToken before caching.
        SaveTokenDataToExternalStorage(accessToken, tokenExpiration);
  
    <span data-ttu-id="48f70-154">Utilisez hello enregistré les valeurs de jeton toocreate MediaServicesCredentials.</span><span class="sxs-lookup"><span data-stu-id="48f70-154">Use hello saved token values toocreate MediaServicesCredentials.</span></span>

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

    <span data-ttu-id="48f70-155">Mettre à jour de copie du jeton hello en cas de mise à jour de jeton de hello en hello Media Services SDK.</span><span class="sxs-lookup"><span data-stu-id="48f70-155">Update hello token copy in case hello token was updated by hello Media Services SDK.</span></span> 

        if(tokenExpiration != context2.Credentials.TokenExpiration)
        {
            UpdateTokenDataInExternalStorageIfNeeded(accessToken, context2.Credentials.TokenExpiration);
        }


* <span data-ttu-id="48f70-156">Si vous avez plusieurs comptes Media Services (par exemple, pour le partage de charge à des fins ou distribution géographique) vous pouvez mettre en cache les objets MediaServicesCredentials à l’aide de la collection de System.Collections.Concurrent.ConcurrentDictionary hello (hello Collection de ConcurrentDictionary représente une collection thread-safe de paires clé/valeur accessibles par plusieurs threads simultanément).</span><span class="sxs-lookup"><span data-stu-id="48f70-156">If you have multiple Media Services accounts (for example, for load sharing purposes or Geo-distribution) you can cache MediaServicesCredentials objects using hello System.Collections.Concurrent.ConcurrentDictionary collection (hello ConcurrentDictionary collection represents a thread-safe collection of key/value pairs that can be accessed by multiple threads concurrently).</span></span> <span data-ttu-id="48f70-157">Vous pouvez ensuite utiliser les informations d’identification de hello GetOrAdd méthode tooget hello mis en cache.</span><span class="sxs-lookup"><span data-stu-id="48f70-157">You can then use hello GetOrAdd method tooget hello cached credentials.</span></span> 
  
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

## <a name="connecting-tooa-media-services-account-located-in-hello-north-china-region"></a><span data-ttu-id="48f70-158">Connexion de compte de service de média tooa situé dans une région hello en Chine du Nord</span><span class="sxs-lookup"><span data-stu-id="48f70-158">Connecting tooa Media Services account located in hello North China region</span></span>
<span data-ttu-id="48f70-159">Si votre compte se trouve dans la région de hello en Chine du Nord, utilisez hello suivant constructeur :</span><span class="sxs-lookup"><span data-stu-id="48f70-159">If your account is located in hello North China region, use hello following constructor:</span></span>

    public CloudMediaContext(Uri apiServer, string accountName, string accountKey, string scope, string acsBaseAddress)

<span data-ttu-id="48f70-160">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="48f70-160">For example:</span></span>

    _context = new CloudMediaContext(
        new Uri("https://wamsbjbclus001rest-hs.chinacloudapp.cn/API/"),
        _mediaServicesAccountName,
        _mediaServicesAccountKey,
        "urn:WindowsAzureMediaServices",
        "https://wamsprodglobal001acs.accesscontrol.chinacloudapi.cn");


## <a name="storing-connection-values-in-configuration"></a><span data-ttu-id="48f70-161">Stockage des valeurs de connexion dans la configuration</span><span class="sxs-lookup"><span data-stu-id="48f70-161">Storing Connection Values in Configuration</span></span>
<span data-ttu-id="48f70-162">Il s’agit d’une valeur de connexion hautement recommandé toostore, notamment les valeurs sensibles telles que votre nom de compte et un mot de passe, dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="48f70-162">It is a highly recommended practice toostore connection values, especially sensitive values such as your account name and password, in configuration.</span></span> <span data-ttu-id="48f70-163">Il est également une données de configuration sensibles tooencrypt pratique recommandée.</span><span class="sxs-lookup"><span data-stu-id="48f70-163">Also, it is a recommended practice tooencrypt sensitive configuration data.</span></span> <span data-ttu-id="48f70-164">Vous pouvez chiffrer le fichier de configuration hello à l’aide de hello Windows EFS (ENCRYPTING file).</span><span class="sxs-lookup"><span data-stu-id="48f70-164">You can encrypt hello entire configuration file by using hello Windows Encrypting File System (EFS).</span></span> <span data-ttu-id="48f70-165">tooenable EFS sur un fichier, avec le bouton hello, sélectionnez **propriétés**et activer le chiffrement Bonjour **avancé** onglet Paramètres. Vous pouvez également créer une solution personnalisée pour le chiffrement des parties sélectionnées d’un fichier de configuration à l’aide de la configuration protégée.</span><span class="sxs-lookup"><span data-stu-id="48f70-165">tooenable EFS on a file, right-click hello file, select **Properties**, and enable encryption in hello **Advanced** settings tab. Or you can create a custom solution for encrypting selected portions of a configuration file by using protected configuration.</span></span> <span data-ttu-id="48f70-166">Consultez la page [Chiffrement des informations de configuration à l'aide de la configuration protégée](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span><span class="sxs-lookup"><span data-stu-id="48f70-166">See [Encrypting Configuration Information Using Protected Configuration](https://msdn.microsoft.com/library/53tyfkaw.aspx).</span></span>

<span data-ttu-id="48f70-167">Hello, le fichier App.config suivant contient des valeurs de connexion hello requis.</span><span class="sxs-lookup"><span data-stu-id="48f70-167">hello following App.config file contains hello required connection values.</span></span> <span data-ttu-id="48f70-168">Hello valeurs Bonjour <appSettings> élément sont les valeurs hello requises que vous avez obtenu à partir du processus d’installation de hello Media Services compte.</span><span class="sxs-lookup"><span data-stu-id="48f70-168">hello values in hello <appSettings> element are hello required values that you got from hello Media Services account setup process.</span></span>

    <configuration>
      <appSettings>
        <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
        <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
      </appSettings>
    </configuration>


<span data-ttu-id="48f70-169">tooretrieve les valeurs de connexion de configuration, vous pouvez utiliser hello **ConfigurationManager** classe, puis affectez toofields de valeurs hello dans votre code :</span><span class="sxs-lookup"><span data-stu-id="48f70-169">tooretrieve connection values from configuration, you can use hello **ConfigurationManager** class and then assign hello values toofields in your code:</span></span>

    private static readonly string _accountName = ConfigurationManager.AppSettings["MediaServicesAccountName"];
    private static readonly string _accountKey = ConfigurationManager.AppSettings["MediaServicesAccountKey"];



## <a name="media-services-learning-paths"></a><span data-ttu-id="48f70-170">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="48f70-170">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="48f70-171">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="48f70-171">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

