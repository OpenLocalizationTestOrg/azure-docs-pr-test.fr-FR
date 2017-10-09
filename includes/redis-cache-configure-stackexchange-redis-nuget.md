<span data-ttu-id="e3a39-101">Applications .NET peuvent utiliser hello **StackExchange.Redis** client de cache, qui peut être configuré dans Visual Studio à l’aide d’un package NuGet qui simplifie la configuration de hello des applications clientes de cache.</span><span class="sxs-lookup"><span data-stu-id="e3a39-101">.NET applications can use hello **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies hello configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="e3a39-102">Pour plus d’informations, consultez hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page et hello [documentation du client de cache StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis#documentation).</span><span class="sxs-lookup"><span data-stu-id="e3a39-102">For more information, see hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  hello [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="e3a39-103">tooconfigure une application cliente dans Visual Studio à l’aide de hello package StackExchange.Redis NuGet, cliquez sur projet hello dans **l’Explorateur de solutions** et choisissez **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e3a39-103">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, right-click hello project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![Manage NuGet packages](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="e3a39-105">Type **StackExchange.Redis** ou **StackExchange.Redis.StrongName** dans la zone de texte de recherche hello, sélectionnez la version souhaitée de hello à partir des résultats de hello, puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="e3a39-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into hello search text box, select hello desired version from hello results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="e3a39-106">Si vous préférez toouse une version de nom fort de hello **StackExchange.Redis** bibliothèque cliente, choisissez **StackExchange.Redis.StrongName**; sinon choisissez **StackExchange.Redis**.</span><span class="sxs-lookup"><span data-stu-id="e3a39-106">If you prefer toouse a strong-named version of hello **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![StackExchange.Redis NuGet package](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="e3a39-108">Hello NuGet package télécharge et ajoute hello obligatoire des références d’assembly pour votre tooaccess d’application client du Cache Redis Azure avec le client de cache StackExchange.Redis hello.</span><span class="sxs-lookup"><span data-stu-id="e3a39-108">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="e3a39-109">Si vous avez précédemment configuré votre projet de toouse StackExchange.Redis, vous pouvez vérifier pour le package toohello de mises à jour à partir de hello **Gestionnaire de Package NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e3a39-109">If you have previously configured your project toouse StackExchange.Redis, you can check for updates toohello package from hello **NuGet Package Manager**.</span></span> <span data-ttu-id="e3a39-110">toocheck pour et les versions d’installation mis à jour de hello package StackExchange.Redis NuGet, cliquez sur **mises à jour** dans Bonjour Bonjour **Gestionnaire de Package NuGet** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e3a39-110">toocheck for and install updated versions of hello StackExchange.Redis NuGet package, click **Updates** in hello hello **NuGet Package Manager** window.</span></span> <span data-ttu-id="e3a39-111">Si un package StackExchange.Redis NuGet de toohello mise à jour est disponible, vous pouvez mettre à jour votre version de hello mis à jour de projet toouse.</span><span class="sxs-lookup"><span data-stu-id="e3a39-111">If an update toohello StackExchange.Redis NuGet package is available, you can update your project toouse hello updated version.</span></span>
> 
> 

<span data-ttu-id="e3a39-112">Vous pouvez également installer hello package StackExchange.Redis NuGet en cliquant sur **Gestionnaire de Package NuGet**, **Package Manager Console** de hello **outils** menu et hello en cours d’exécution commande suivante à partir de hello **Package Manager Console** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="e3a39-112">You can also install hello StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu, and running hello following command from hello **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```
