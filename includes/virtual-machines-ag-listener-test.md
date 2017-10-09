Dans cette étape, vous testez écouteur hello à l’aide d’une application cliente qui s’exécute sur hello même réseau.

Connectivité client a hello suivant les exigences :

* Écouteur de toohello de connexions client doit provenir de machines qui résident dans un service cloud différent hello une que hôtes hello réplicas de disponibilité Always On.
* Si hello toujours sur les réplicas se trouvent dans des sous-réseaux différents, les clients doivent spécifier *MultisubnetFailover = True* dans la chaîne de connexion hello. Les résultats de cette condition de connexion parallèle tentatives tooreplicas Bonjour différents sous-réseaux. Ce scénario inclut un déploiement de groupe de disponibilité AlwaysOn dans plusieurs régions.

Par exemple, l’écouteur de toohello tooconnect à partir d’une des machines virtuelles de hello Bonjour même réseau virtuel Azure (mais pas un serveur qui héberge un réplica). Un moyen simple de toocomplete ce test est écouteur toohello tootry tooconnect SQL Server Management Studio. Une autre méthode simple est toorun [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx), comme suit :

    sqlcmd -S "<ListenerName>,<EndpointPort>" -d "<DatabaseName>" -Q "select @@servername, db_name()" -l 15

> [!NOTE]
> Si hello EndpointPort valeur est *1433*, vous n’êtes pas toospecify requis dans l’appel de hello. Hello appel précédent suppose également que l’ordinateur client hello est toohello joints à un même domaine et que l’appelant hello dispose des autorisations sur la base de données hello à l’aide de l’authentification Windows.
> 
> 

Lorsque vous testez le port d’écoute hello, être toofail que via toomake de groupe de disponibilité hello assurer que les clients peuvent se connecter à toohello écouteur à un autre.

