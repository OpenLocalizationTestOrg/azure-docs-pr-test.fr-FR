## <a name="set-up-your-development-environment"></a>Configuration de l'environnement de développement
Ensuite, configurez votre environnement de développement dans Visual Studio afin de vous êtes prêt tootry exemples de code hello dans ce guide.

### <a name="create-a-windows-console-application-project"></a>Créer un projet d’application de console Windows
Dans Visual Studio, créez une application de console Windows. Hello suit vous montre comment toocreate une application de console dans Visual Studio 2017, toutefois, les étapes de hello sont similaires dans les autres versions de Visual Studio.

1. Sélectionnez **Fichier** > **Nouveau** > **Projet**
2. Sélectionnez **Installé** > **Modèles** > **Visual C#** > **Bureau classique Windows**
3. Sélectionnez **Application console (.NET Framework)**
4. Entrez un nom pour votre application dans hello **nom :** champ
5. Sélectionnez **OK**.

![Boîte de dialogue Création du projet dans Visual Studio](./media/storage-development-environment-include/storage-development-environment-include-1.png)

Tous les exemples de code dans ce didacticiel peuvent être ajoutés toohello `Main()` méthode de votre application de console `Program.cs` fichier.

Vous pouvez utiliser hello bibliothèque cliente de stockage Azure dans n’importe quel type d’application .NET, y compris une application web ou de service cloud Azure et les applications de bureau et mobiles. Dans ce guide, nous utilisons une application console pour plus de simplicité.

### <a name="use-nuget-tooinstall-hello-required-packages"></a>Utiliser les packages NuGet tooinstall hello requis
Il existe deux packages, vous devez tooreference dans votre projet toocomplete ce didacticiel :

* [Bibliothèque cliente Microsoft Azure Storage pour .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): ce package fournit un accès par programmation toodata des ressources dans votre compte de stockage.
* [Bibliothèque Microsoft Azure Configuration Manager pour .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) : ce package fournit une classe pour l’analyse d’une chaîne de connexion à partir d’un fichier de configuration, quel que soit l’emplacement d’exécution de votre application.

Vous pouvez utiliser NuGet tooobtain les deux packages. Procédez comme suit :

1. Cliquez avec le bouton droit sur votre projet dans **l’Explorateur de solutions**, puis sélectionnez **Gérer les packages NuGet**.
2. Rechercher en ligne du terme « WindowsAzure.Storage » et cliquez sur **installer** tooinstall hello bibliothèque cliente de stockage et de ses dépendances.
3. Rechercher en ligne « WindowsAzure.ConfigurationManager » et cliquez sur **installer** tooinstall hello Azure Configuration Manager.

> [!NOTE]
> package de bibliothèque cliente de stockage Hello est également inclus dans hello [Azure SDK pour .NET](https://azure.microsoft.com/downloads/). Toutefois, nous vous recommandons d’installer également hello bibliothèque cliente de stockage tooensure NuGet que vous disposez toujours de version la plus récente de la bibliothèque cliente de hello hello.
> 
> dépendances ODataLib de Hello Bonjour bibliothèque cliente de stockage pour .NET sont résolus par les packages ODataLib de hello disponibles sur NuGet, et non à partir des Services de données WCF. les bibliothèques ODataLib Hello peuvent être téléchargés directement ou référencés par votre projet de code via NuGet. les packages ODataLib spécifiques Hello utilisés par la bibliothèque cliente de stockage de hello sont [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/), et [Spatial](http://nuget.org/packages/System.Spatial/). Alors que ces bibliothèques sont utilisées par les classes de stockage de Table Azure hello, ils sont les dépendances requises pour la programmation avec hello bibliothèque cliente de stockage.
> 
> 

### <a name="determine-your-target-environment"></a>Déterminer votre environnement cible
Vous avez deux options d’environnement pour l’exécution des exemples de hello dans ce guide :

* Vous pouvez exécuter votre code par rapport à un compte de stockage Azure dans le cloud de hello. 
* Vous pouvez exécuter votre code par rapport à l’émulateur de stockage Azure hello. l’émulateur de stockage Hello est un environnement local qui émule un compte de stockage Azure dans le cloud de hello. l’émulateur Hello est une option disponible pour tester et déboguer votre code pendant que votre application est en cours de développement. émulateur de Hello utilise un compte bien connu et une clé. Pour plus d’informations, consultez [hello d’utilisation émulateur de stockage pour le développement et le test](../articles/storage/common/storage-use-emulator.md)

Si vous ciblez un compte de stockage dans le cloud de hello, copiez la clé d’accès primaire hello pour votre compte de stockage à partir de hello portail Azure. Pour plus d’informations, voir [Affichage et copie de clés d’accès de stockage](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys).

> [!NOTE]
> Vous pouvez cibler tooavoid d’émulateur de stockage hello encourir les coûts associés au stockage Azure. Toutefois, si vous choisissez tootarget un compte de stockage Azure dans le cloud de hello, les coûts pour effectuer ce didacticiel sera négligeables.
> 
> 

### <a name="configure-your-storage-connection-string"></a>Configurer votre chaîne de connexion de stockage
Hello bibliothèque cliente de stockage Azure pour .NET prend en charge de l’aide d’un points de terminaison de stockage connexion chaîne tooconfigure et informations d’identification pour accéder aux services de stockage. Hello meilleure manière toomaintain votre chaîne de connexion de stockage est dans un fichier de configuration. 

Pour plus d’informations sur les chaînes de connexion, consultez [configurer une chaîne de connexion de tooAzure stockage](../articles/storage/common/storage-configure-connection-string.md).

> [!NOTE]
> Votre clé de compte de stockage est similaire toohello racine mot de passe pour votre compte de stockage. Toujours être prudent tooprotect votre clé de compte de stockage. Éviter la distribution des utilisateurs tooother, le codage en dur, ou l’enregistrer dans un fichier texte brut qui est accessible tooothers. Régénérez votre clé à l’aide de hello portail Azure si vous pensez qu’il a peut-être été compromis.
> 
> 

tooconfigure votre chaîne de connexion, l’ouvrir hello `app.config` fichier à partir de l’Explorateur de solutions dans Visual Studio. Ajouter du contenu hello Hello `<appSettings>` élément indiqué ci-dessous. Remplacez `account-name` avec nom hello de votre compte de stockage et `account-key` avec votre clé d’accès de compte :

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key" />
    </appSettings>
</configuration>
```

Par exemple, votre paramètre de configuration est semblable à :

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=GMuzNHjlB3S9itqZJHHCnRkrokLkcSyW7yK9BRbGp0ENePunLPwBgpxV1Z/pVo9zpem/2xSHXkMqTHHLcx8XRA==" />
```

émulateur de stockage tootarget hello, vous pouvez utiliser un raccourci qui mappe une clé et le nom de compte bien connu toohello. Dans ce cas, le paramètre de votre chaîne de connexion est :

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

