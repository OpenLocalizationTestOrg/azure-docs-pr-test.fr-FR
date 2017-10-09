toocreate un cache, d’abord vous connecter toohello [portail Azure](https://portal.azure.com), puis cliquez sur **nouveau** > **bases de données** > **leCacheRedis**.

> [!NOTE]
> Si vous ne possédez pas de compte Azure, vous pouvez [ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) en quelques minutes.
> 
> 

![New cache](media/redis-cache-create/redis-cache-new-cache-menu.png)

> [!NOTE]
> En outre toocreating met en cache dans hello portail Azure, vous pouvez également les créer à l’aide du Gestionnaire de ressources modèles, PowerShell ou CLI d’Azure.
> 
> * toocreate un cache à l’aide des modèles du Gestionnaire de ressources, consultez [créer un cache Redis à l’aide d’un modèle](../articles/redis-cache/cache-redis-cache-arm-provision.md).
> * toocreate un cache à l’aide d’Azure PowerShell, consultez [gérer le Cache Redis Azure avec Azure PowerShell](../articles/redis-cache/cache-howto-manage-redis-cache-powershell.md).
> * toocreate un cache à l’aide de CLI d’Azure, consultez [comment toocreate et gérer le Cache Redis Azure à l’aide de hello Azure Interface de ligne (Azure)](../articles/redis-cache/cache-manage-cli.md).
> 
> 

Bonjour **nouveau Cache Redis** panneau, spécifiez hello la configuration souhaitée pour le cache de hello.

![Create cache](media/redis-cache-create/redis-cache-cache-create.png) 

* Dans **nom Dns**, entrez un toouse de nom de cache unique pour le point de terminaison de cache hello. nom du cache Hello doit être une chaîne comprise entre 1 et 63 caractères et contenir uniquement des chiffres, des lettres et hello `-` caractère. Hello nom du cache ne peut pas commencer ni se terminer par hello `-` caractère et consécutifs `-` caractères ne sont pas valides.
* Pour **abonnement**, sélectionnez hello abonnement Azure que vous souhaitez toouse pour le cache de hello. Si votre compte n'est qu’un seul abonnement, il sera automatiquement sélectionné et hello **abonnement** s’affichera pas de liste déroulante.
* Dans **Groupe de ressources**, sélectionnez ou créez un groupe de ressources pour le cache. Pour plus d’informations, consultez [à l’aide de la ressource groupes toomanage vos ressources Azure](../articles/azure-resource-manager/resource-group-overview.md). 
* Utilisez **emplacement** toospecify hello emplacement géographique dans lequel votre cache est hébergé. Pour de meilleures performances de hello, Microsoft recommande vivement de créer le cache de hello dans hello même région que l’application de client de cache hello.
* Utilisez **niveau tarifaire** tooselect hello souhaité la taille du cache et fonctionnalités.
* **Redis cluster** vous permet de caches de toocreate supérieure à 53 Go et tooshard des données sur plusieurs nœuds de Redis. Pour plus d’informations, consultez [comment tooconfigure clustering Premium Azure Redis cache](../articles/redis-cache/cache-how-to-premium-clustering.md).
* **Persistance de redis** offre hello capacité toopersist votre tooan cache compte de stockage Azure. Pour obtenir des instructions sur la configuration de la persistance, consultez [la persistance tooconfigure cache Redis Azure Premium](../articles/redis-cache/cache-how-to-premium-persistence.md).
* **Réseau virtuel** fournit une meilleure sécurité et isolation en limitant l’accès tooyour cache tooonly ces clients dans hello spécifié réseau virtuel Azure. Vous pouvez utiliser toutes les fonctionnalités de hello de réseau virtuel tels que les sous-réseaux, les stratégies de contrôle d’accès et les autres toofurther fonctionnalités restreignent l’accès tooRedis. Pour plus d’informations, consultez [comment tooconfigure réseau virtuel prend en charge un Premium Azure Redis cache](../articles/redis-cache/cache-how-to-premium-vnet.md).
* Par défaut, l’accès non SSL est désactivé pour les nouveaux caches. port non-SSL de hello tooenable, cocher **débloquer le port 6379 (pas chiffrées SSL)**.

Une fois les nouvelles options de cache hello sont configurées, cliquez sur **créer**. Il peut prendre quelques minutes pour hello cache toobe est créé. état de hello toocheck, vous pouvez surveiller progression hello sur le tableau d’accueil hello. Une fois le cache de hello a été créé, votre nouveau cache a un **en cours d’exécution** état et est prêt pour une utilisation avec [paramètres par défaut](../articles/redis-cache/cache-configure.md#default-redis-server-configuration).

![Cache created](media/redis-cache-create/redis-cache-cache-created.png)

