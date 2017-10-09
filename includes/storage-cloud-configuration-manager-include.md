<span data-ttu-id="0a2f3-101">Hello [bibliothèque du Gestionnaire de Configuration de Microsoft Azure pour .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) fournit une classe pour l’analyse d’une chaîne de connexion à partir d’un fichier de configuration.</span><span class="sxs-lookup"><span data-stu-id="0a2f3-101">hello [Microsoft Azure Configuration Manager Library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) provides a class for parsing a connection string from a configuration file.</span></span> <span data-ttu-id="0a2f3-102">Hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) classe analyse les paramètres de configuration qu’application de client hello soit en sur hello bureau, sur un appareil mobile, dans une machine virtuelle Azure, ou dans un service cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="0a2f3-102">hello [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/mt634650.aspx) class parses configuration settings regardless of whether hello client application is running on hello desktop, on a mobile device, in an Azure virtual machine, or in an Azure cloud service.</span></span>

<span data-ttu-id="0a2f3-103">tooreference hello CloudConfigurationManager package, ajoutez hello `using` directive :</span><span class="sxs-lookup"><span data-stu-id="0a2f3-103">tooreference hello CloudConfigurationManager package, add hello following `using` directive:</span></span>

```csharp
using Microsoft.Azure; //Namespace for CloudConfigurationManager
```

<span data-ttu-id="0a2f3-104">Voici un exemple qui montre comment tooretrieve une chaîne de connexion à partir d’un fichier de configuration :</span><span class="sxs-lookup"><span data-stu-id="0a2f3-104">Here's an example that shows how tooretrieve a connection string from a configuration file:</span></span>

```csharp
// Parse hello connection string and return a reference toohello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
```

<span data-ttu-id="0a2f3-105">À l’aide de hello Azure Configuration Manager est facultative.</span><span class="sxs-lookup"><span data-stu-id="0a2f3-105">Using hello Azure Configuration Manager is optional.</span></span> <span data-ttu-id="0a2f3-106">Vous pouvez également utiliser une API comme hello du .NET Framework [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="0a2f3-106">You can also use an API like hello .NET Framework's [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager.aspx) class.</span></span>

