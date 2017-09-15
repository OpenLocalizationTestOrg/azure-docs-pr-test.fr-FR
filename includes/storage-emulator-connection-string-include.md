<span data-ttu-id="dad14-101">L’émulateur de stockage prend en charge uniquement un compte fixe et une clé d’authentification connue pour l’authentification par clé partagée.</span><span class="sxs-lookup"><span data-stu-id="dad14-101">The storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="dad14-102">Ce compte et cette clé sont les seules informations d’identification par clé partagée autorisées pour une utilisation avec l’émulateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="dad14-102">This account and key are the only Shared Key credentials permitted for use with the storage emulator.</span></span> <span data-ttu-id="dad14-103">Il s'agit de :</span><span class="sxs-lookup"><span data-stu-id="dad14-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="dad14-104">La clé d'authentification prise en charge par l'émulateur de stockage est destinée uniquement au test de la fonctionnalité de votre code d'authentification du client.</span><span class="sxs-lookup"><span data-stu-id="dad14-104">The authentication key supported by the storage emulator is intended only for testing the functionality of your client authentication code.</span></span> <span data-ttu-id="dad14-105">Elle n'offre aucune fonction de sécurité.</span><span class="sxs-lookup"><span data-stu-id="dad14-105">It does not serve any security purpose.</span></span> <span data-ttu-id="dad14-106">Vous ne pouvez pas utiliser votre compte et votre clé de stockage de production avec l'émulateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="dad14-106">You cannot use your production storage account and key with the storage emulator.</span></span> <span data-ttu-id="dad14-107">Vous ne devez pas utiliser le compte de développement avec des données de production.</span><span class="sxs-lookup"><span data-stu-id="dad14-107">You should not use the development account with production data.</span></span>
> 
> <span data-ttu-id="dad14-108">L’émulateur de stockage prend uniquement en charge la connexion via le protocole HTTP.</span><span class="sxs-lookup"><span data-stu-id="dad14-108">The storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="dad14-109">Toutefois, HTTPS est le protocole recommandé pour l’accès aux ressources dans un compte de Stockage Azure de production.</span><span class="sxs-lookup"><span data-stu-id="dad14-109">However, HTTPS is the recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-to-the-emulator-account-using-a-shortcut"></a><span data-ttu-id="dad14-110">Se connecter au compte de l’émulateur à l’aide d’un raccourci</span><span class="sxs-lookup"><span data-stu-id="dad14-110">Connect to the emulator account using a shortcut</span></span>
<span data-ttu-id="dad14-111">Le moyen le plus simple de vous connecter à l’émulateur de stockage à partir de votre application est de configurer une chaîne de connexion dans le fichier de configuration de votre application qui référence le raccourci `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="dad14-111">The easiest way to connect to the storage emulator from your application is to configure a connection string in your application's configuration file that references the shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="dad14-112">Voici un exemple de chaîne de connexion à l’émulateur de stockage dans un fichier *app.config* :</span><span class="sxs-lookup"><span data-stu-id="dad14-112">Here's an example of a connection string to the storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-to-the-emulator-account-using-the-well-known-account-name-and-key"></a><span data-ttu-id="dad14-113">Se connecter au compte de l’émulateur à l’aide d’un nom de compte connu et d’une clé</span><span class="sxs-lookup"><span data-stu-id="dad14-113">Connect to the emulator account using the well-known account name and key</span></span>
<span data-ttu-id="dad14-114">Pour créer une chaîne de connexion qui référence le nom et la clé du compte de l’émulateur, vous devez définir les points de terminaison associés aux services que vous souhaitez utiliser à partir de l’émulateur dans la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="dad14-114">To create a connection string that references the emulator account name and key, you must specify the endpoints for each of the services you wish to use from the emulator in the connection string.</span></span> <span data-ttu-id="dad14-115">Cela est nécessaire pour que la chaîne de connexion puisse référencer les points de terminaison de l’émulateur, qui sont différents de ceux associés à un compte de stockage de production.</span><span class="sxs-lookup"><span data-stu-id="dad14-115">This is necessary so that the connection string will reference the emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="dad14-116">Par exemple, la valeur de votre chaîne de connexion ressemblera à ceci :</span><span class="sxs-lookup"><span data-stu-id="dad14-116">For example, the value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="dad14-117">Cette valeur est identique au raccourci présenté plus haut, `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="dad14-117">This value is identical to the shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="dad14-118">Spécifier un proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="dad14-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="dad14-119">Vous pouvez aussi spécifier un proxy HTTP à utiliser lorsque vous testez votre service sur l’émulateur de stockage.</span><span class="sxs-lookup"><span data-stu-id="dad14-119">You can also specify an HTTP proxy to use when you're testing your service against the storage emulator.</span></span> <span data-ttu-id="dad14-120">Cela peut être utile pour observer les demandes et les réponses HTTP pendant que vous déboguez des opérations sur les services de stockage.</span><span class="sxs-lookup"><span data-stu-id="dad14-120">This can be useful for observing HTTP requests and responses while you're debugging operations against the storage services.</span></span> <span data-ttu-id="dad14-121">Pour spécifier un proxy, ajoutez l’option `DevelopmentStorageProxyUri` à la chaîne de connexion, puis définissez sa valeur sur l’URI du proxy.</span><span class="sxs-lookup"><span data-stu-id="dad14-121">To specify a proxy, add the `DevelopmentStorageProxyUri` option to the connection string, and set its value to the proxy URI.</span></span> <span data-ttu-id="dad14-122">Voici par exemple une chaîne de connexion qui pointe vers l’émulateur de stockage et configure un proxy HTTP :</span><span class="sxs-lookup"><span data-stu-id="dad14-122">For example, here is a connection string that points to the storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

