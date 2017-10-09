Applications .NET peuvent utiliser hello **StackExchange.Redis** client de cache, qui peut être configuré dans Visual Studio à l’aide d’un package NuGet qui simplifie la configuration de hello des applications clientes de cache. 

> [!NOTE]
> Pour plus d’informations, consultez hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page et hello [documentation du client de cache StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis#documentation).
> 
> 

tooconfigure une application cliente dans Visual Studio à l’aide de hello package StackExchange.Redis NuGet, cliquez sur projet hello dans **l’Explorateur de solutions** et choisissez **gérer les Packages NuGet**. 

![Manage NuGet packages](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

Type **StackExchange.Redis** ou **StackExchange.Redis.StrongName** dans la zone de texte de recherche hello, sélectionnez la version souhaitée de hello à partir des résultats de hello, puis cliquez sur **installer**.

> [!NOTE]
> Si vous préférez toouse une version de nom fort de hello **StackExchange.Redis** bibliothèque cliente, choisissez **StackExchange.Redis.StrongName**; sinon choisissez **StackExchange.Redis**.
> 
> 

![StackExchange.Redis NuGet package](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

Hello NuGet package télécharge et ajoute hello obligatoire des références d’assembly pour votre tooaccess d’application client du Cache Redis Azure avec le client de cache StackExchange.Redis hello.

> [!NOTE]
> Si vous avez précédemment configuré votre projet de toouse StackExchange.Redis, vous pouvez vérifier pour le package toohello de mises à jour à partir de hello **Gestionnaire de Package NuGet**. toocheck pour et les versions d’installation mis à jour de hello package StackExchange.Redis NuGet, cliquez sur **mises à jour** dans Bonjour Bonjour **Gestionnaire de Package NuGet** fenêtre. Si un package StackExchange.Redis NuGet de toohello mise à jour est disponible, vous pouvez mettre à jour votre version de hello mis à jour de projet toouse.
> 
> 

Vous pouvez également installer hello package StackExchange.Redis NuGet en cliquant sur **Gestionnaire de Package NuGet**, **Package Manager Console** de hello **outils** menu et hello en cours d’exécution commande suivante à partir de hello **Package Manager Console** fenêtre.
    
```
Install-Package StackExchange.Redis
```
