Hello [bibliothèque du Gestionnaire de Configuration de Microsoft Azure pour .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) fournit une classe pour l’analyse d’une chaîne de connexion à partir d’un fichier de configuration. Hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) classe analyse les paramètres de configuration qu’application de client hello soit en sur hello bureau, sur un appareil mobile, dans une machine virtuelle Azure, ou dans un service cloud Azure.

tooreference hello CloudConfigurationManager package, ajoutez hello `using` directive :

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

Voici un exemple qui montre comment tooretrieve une chaîne de connexion à partir d’un fichier de configuration :

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

À l’aide de hello Azure Configuration Manager est facultative. Vous pouvez également utiliser une API comme hello du .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) classe.

