l’émulateur de stockage Hello prend en charge un seul compte fixe et une clé d’authentification connu pour l’authentification Shared Key. Ce compte et sa clé sont hello uniquement la clé partagée informations d’identification autorisées pour une utilisation avec l’émulateur de stockage hello. Il s'agit de :

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> clé d’authentification Hello pris en charge par l’émulateur de stockage hello est prévu uniquement pour les fonctionnalités de hello test de votre code d’authentification client. Elle n'offre aucune fonction de sécurité. Vous ne pouvez pas utiliser votre compte de stockage de production et votre clé avec l’émulateur de stockage hello. Vous ne devez pas utiliser compte de développement hello avec les données de production.
> 
> l’émulateur de stockage Hello prend en charge la connexion via le protocole HTTP uniquement. Toutefois, le protocole HTTPS est hello recommandé de protocole pour accéder aux ressources dans un compte de stockage Azure de production.
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a>Se connecter à l’aide d’un raccourci compte de l’émulateur toohello
Hello plus simple façon tooconnect toohello l’émulateur de stockage à partir de votre application est tooconfigure une chaîne de connexion dans le fichier de configuration de votre application qui fait référence à des raccourcis de hello `UseDevelopmentStorage=true`. Voici un exemple d’un émulateur de stockage toohello chaîne connexion dans une *app.config* fichier : 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a>Connexion de compte d’émulateur toohello à l’aide de la clé et le nom de compte bien connu hello
toocreate une chaîne de connexion que références hello nom de compte d’émulateur et clé, vous devez spécifier les points de terminaison hello pour chacun des hello services que vous souhaitez toouse à partir de l’émulateur hello dans la chaîne de connexion hello. Cela est nécessaire afin que la chaîne de connexion hello référencera hello émulateur points de terminaison qui sont différentes de celles d’un compte de stockage de production. Par exemple, valeur hello votre chaîne de connexion ressemble à ceci :

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

Cette valeur est contextuel toohello identiques illustrée ci-dessus, `UseDevelopmentStorage=true`.

#### <a name="specify-an-http-proxy"></a>Spécifier un proxy HTTP
Vous pouvez également spécifier un toouse de proxy HTTP lorsque vous testez votre service sur l’émulateur de stockage hello. Cela peut être utile pour observer les requêtes et réponses HTTP pendant que vous déboguez des opérations sur les services de stockage hello. toospecify un proxy, ajoutez hello `DevelopmentStorageProxyUri` option de chaîne de connexion toohello et définissez son URI de proxy toohello valeur. Par exemple, voici une chaîne de connexion qui pointe l’émulateur de stockage toohello et configure un proxy HTTP :

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

