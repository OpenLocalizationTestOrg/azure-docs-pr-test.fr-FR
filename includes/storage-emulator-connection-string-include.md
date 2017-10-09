<span data-ttu-id="1dc79-101">l’émulateur de stockage Hello prend en charge un seul compte fixe et une clé d’authentification connu pour l’authentification Shared Key.</span><span class="sxs-lookup"><span data-stu-id="1dc79-101">hello storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="1dc79-102">Ce compte et sa clé sont hello uniquement la clé partagée informations d’identification autorisées pour une utilisation avec l’émulateur de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="1dc79-102">This account and key are hello only Shared Key credentials permitted for use with hello storage emulator.</span></span> <span data-ttu-id="1dc79-103">Il s'agit de :</span><span class="sxs-lookup"><span data-stu-id="1dc79-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="1dc79-104">clé d’authentification Hello pris en charge par l’émulateur de stockage hello est prévu uniquement pour les fonctionnalités de hello test de votre code d’authentification client.</span><span class="sxs-lookup"><span data-stu-id="1dc79-104">hello authentication key supported by hello storage emulator is intended only for testing hello functionality of your client authentication code.</span></span> <span data-ttu-id="1dc79-105">Elle n'offre aucune fonction de sécurité.</span><span class="sxs-lookup"><span data-stu-id="1dc79-105">It does not serve any security purpose.</span></span> <span data-ttu-id="1dc79-106">Vous ne pouvez pas utiliser votre compte de stockage de production et votre clé avec l’émulateur de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="1dc79-106">You cannot use your production storage account and key with hello storage emulator.</span></span> <span data-ttu-id="1dc79-107">Vous ne devez pas utiliser compte de développement hello avec les données de production.</span><span class="sxs-lookup"><span data-stu-id="1dc79-107">You should not use hello development account with production data.</span></span>
> 
> <span data-ttu-id="1dc79-108">l’émulateur de stockage Hello prend en charge la connexion via le protocole HTTP uniquement.</span><span class="sxs-lookup"><span data-stu-id="1dc79-108">hello storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="1dc79-109">Toutefois, le protocole HTTPS est hello recommandé de protocole pour accéder aux ressources dans un compte de stockage Azure de production.</span><span class="sxs-lookup"><span data-stu-id="1dc79-109">However, HTTPS is hello recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a><span data-ttu-id="1dc79-110">Se connecter à l’aide d’un raccourci compte de l’émulateur toohello</span><span class="sxs-lookup"><span data-stu-id="1dc79-110">Connect toohello emulator account using a shortcut</span></span>
<span data-ttu-id="1dc79-111">Hello plus simple façon tooconnect toohello l’émulateur de stockage à partir de votre application est tooconfigure une chaîne de connexion dans le fichier de configuration de votre application qui fait référence à des raccourcis de hello `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="1dc79-111">hello easiest way tooconnect toohello storage emulator from your application is tooconfigure a connection string in your application's configuration file that references hello shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="1dc79-112">Voici un exemple d’un émulateur de stockage toohello chaîne connexion dans une *app.config* fichier :</span><span class="sxs-lookup"><span data-stu-id="1dc79-112">Here's an example of a connection string toohello storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a><span data-ttu-id="1dc79-113">Connexion de compte d’émulateur toohello à l’aide de la clé et le nom de compte bien connu hello</span><span class="sxs-lookup"><span data-stu-id="1dc79-113">Connect toohello emulator account using hello well-known account name and key</span></span>
<span data-ttu-id="1dc79-114">toocreate une chaîne de connexion que références hello nom de compte d’émulateur et clé, vous devez spécifier les points de terminaison hello pour chacun des hello services que vous souhaitez toouse à partir de l’émulateur hello dans la chaîne de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="1dc79-114">toocreate a connection string that references hello emulator account name and key, you must specify hello endpoints for each of hello services you wish toouse from hello emulator in hello connection string.</span></span> <span data-ttu-id="1dc79-115">Cela est nécessaire afin que la chaîne de connexion hello référencera hello émulateur points de terminaison qui sont différentes de celles d’un compte de stockage de production.</span><span class="sxs-lookup"><span data-stu-id="1dc79-115">This is necessary so that hello connection string will reference hello emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="1dc79-116">Par exemple, valeur hello votre chaîne de connexion ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="1dc79-116">For example, hello value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="1dc79-117">Cette valeur est contextuel toohello identiques illustrée ci-dessus, `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="1dc79-117">This value is identical toohello shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="1dc79-118">Spécifier un proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="1dc79-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="1dc79-119">Vous pouvez également spécifier un toouse de proxy HTTP lorsque vous testez votre service sur l’émulateur de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="1dc79-119">You can also specify an HTTP proxy toouse when you're testing your service against hello storage emulator.</span></span> <span data-ttu-id="1dc79-120">Cela peut être utile pour observer les requêtes et réponses HTTP pendant que vous déboguez des opérations sur les services de stockage hello.</span><span class="sxs-lookup"><span data-stu-id="1dc79-120">This can be useful for observing HTTP requests and responses while you're debugging operations against hello storage services.</span></span> <span data-ttu-id="1dc79-121">toospecify un proxy, ajoutez hello `DevelopmentStorageProxyUri` option de chaîne de connexion toohello et définissez son URI de proxy toohello valeur.</span><span class="sxs-lookup"><span data-stu-id="1dc79-121">toospecify a proxy, add hello `DevelopmentStorageProxyUri` option toohello connection string, and set its value toohello proxy URI.</span></span> <span data-ttu-id="1dc79-122">Par exemple, voici une chaîne de connexion qui pointe l’émulateur de stockage toohello et configure un proxy HTTP :</span><span class="sxs-lookup"><span data-stu-id="1dc79-122">For example, here is a connection string that points toohello storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

