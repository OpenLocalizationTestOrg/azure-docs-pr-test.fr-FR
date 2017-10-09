---
title: "aaaGet main hello bibliothèque du CDN Azure pour .NET | Documents Microsoft"
description: "Découvrez comment toowrite .NET applications toomanage CDN Azure à l’aide de Visual Studio."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 63cf4101-92e7-49dd-a155-a90e54a792ca
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9753e48c7469072cef6b2ac728e18c78121c97f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a>Prise en main du développement Azure CDN
> [!div class="op_single_selector"]
> * [Node.JS](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

Vous pouvez utiliser hello [bibliothèque du CDN Azure pour .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate création et la gestion des profils CDN et des points de terminaison.  Ce didacticiel guide dans la création d’une application console .NET simple qui illustre plusieurs opérations disponibles de hello hello.  Ce didacticiel n’est pas conçu toodescribe tous les aspects de hello Azure CDN bibliothèque pour .NET en détail.

Vous avez besoin de Visual Studio 2015 toocomplete ce didacticiel.  [Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) est disponible gratuitement en téléchargement.

> [!TIP]
> Hello [projet achevé de ce didacticiel](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) est disponible pour téléchargement sur MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a>Créer votre projet et ajouter des packages Nuget
Maintenant que nous avons créé un groupe de ressources pour les profils de notre CDN et donné notre profils CDN toomanage d’autorisation d’application Azure AD et les points de terminaison de ce groupe, nous pouvons commencer à créer notre application.

Dans Visual Studio 2015, cliquez sur **fichier**, **nouveau**, **projet...**  tooopen hello nouvelle boîte de dialogue projet.  Développez **Visual C#**, puis sélectionnez **Windows** dans le volet gauche de hello hello.  Cliquez sur **Application Console** dans le volet central de hello.  Nommez votre projet, puis cliquez sur **OK**.  

![Nouveau projet](./media/cdn-app-dev-net/cdn-new-project.png)

Notre projet va toouse certaines bibliothèques Azure contenues dans les packages Nuget.  Vous allez ajouter ces projets toohello.

1. Cliquez sur hello **outils** menu, **Gestionnaire de Package Nuget**, puis **Package Manager Console**.
   
    ![Gérer les packages NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. Dans la Console du Gestionnaire de Package de hello, exécutez hello suivant commande tooinstall hello **Active Directory Authentication Library (ADAL)**:
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. Exécutez hello suivant tooinstall hello **bibliothèque de gestion Azure CDN**:
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a>Directives, constantes, méthode principale et méthodes d’assistance
Passons la structure de base hello de notre programme écrit.

1. Dans l’onglet de Program.cs hello, remplacez hello `using` directives haut hello, avec les éléments suivants de hello :
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using Microsoft.Azure.Management.Cdn;
    using Microsoft.Azure.Management.Cdn.Models;
    using Microsoft.Azure.Management.Resources;
    using Microsoft.Azure.Management.Resources.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```
2. Nous devons toodefine certaines constantes que nos méthodes utilisera.  Bonjour `Program` (classe), mais avant l’exécution hello `Main` méthode, ajoutez hello qui suit.  Être tooreplace que des espaces réservés de hello, y compris hello  **&lt;crochets pointus&gt;**, avec vos propres valeurs en fonction des besoins.
   
    ```csharp
    //Tenant app constants
    private const string clientID = "<YOUR CLIENT ID>";
    private const string clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    private const string authority = "https://login.microsoftonline.com/<YOUR TENANT ID>/<YOUR TENANT DOMAIN NAME>";
   
    //Application constants
    private const string subscriptionId = "<YOUR SUBSCRIPTION ID>";
    private const string profileName = "CdnConsoleApp";
    private const string endpointName = "<A UNIQUE NAME FOR YOUR CDN ENDPOINT>";
    private const string resourceGroupName = "CdnConsoleTutorial";
    private const string resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. Également au niveau de classe hello, vous devez définir ces deux variables.  Nous allons utiliser ces toodetermine ultérieure si notre profil et le point de terminaison existent déjà.
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. Remplacez hello `Main` méthode comme suit :
   
   ```csharp
   static void Main(string[] args)
   {
       //Get a token
       AuthenticationResult authResult = GetAccessToken();
   
       // Create CDN client
       CdnManagementClient cdn = new CdnManagementClient(new TokenCredentials(authResult.AccessToken))
           { SubscriptionId = subscriptionId };
   
       ListProfilesAndEndpoints(cdn);
   
       // Create CDN Profile
       CreateCdnProfile(cdn);
   
       // Create CDN Endpoint
       CreateCdnEndpoint(cdn);
   
       Console.WriteLine();
   
       // Purge CDN Endpoint
       PromptPurgeCdnEndpoint(cdn);
   
       // Delete CDN Endpoint
       PromptDeleteCdnEndpoint(cdn);
   
       // Delete CDN Profile
       PromptDeleteCdnProfile(cdn);
   
       Console.WriteLine("Press Enter tooend program.");
       Console.ReadLine();
   }
   ```
5. Certaines de nos autres méthodes vont utilisateur de hello tooprompt des questions de « Oui/non ».  Ajouter hello suivant de méthode toomake qui un peu plus simple :
   
    ```csharp
    private static bool PromptUser(string Question)
    {
        Console.Write(Question + " (Y/N): ");
        var response = Console.ReadKey();
        Console.WriteLine();
        if (response.Key == ConsoleKey.Y)
        {
            return true;
        }
        else if (response.Key == ConsoleKey.N)
        {
            return false;
        }
        else
        {
            // They pressed something other than Y or N.  Let's ask them again.
            return PromptUser(Question);
        }
    }
    ```

Maintenant que la structure de base hello de notre programme est écrit, nous devons créer des méthodes de hello appelées par hello `Main` (méthode).

## <a name="authentication"></a>Authentification
Avant de pouvoir utiliser hello bibliothèque de gestion Azure CDN, vous avez besoin tooauthenticate notre service principal et obtenir un jeton d’authentification.  Cette méthode utilise le jeton de hello tooretrieve ADAL.

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority); 
    ClientCredential credential = new ClientCredential(clientID, clientSecret);
    AuthenticationResult authResult = 
        authContext.AcquireTokenAsync("https://management.core.windows.net/", credential).Result;

    return authResult;
}
```

Si vous utilisez l’authentification des utilisateurs individuels, hello `GetAccessToken` méthode aura un aspect légèrement différente.

> [!IMPORTANT]
> Utilisez uniquement cet exemple de code si vous choisissez l’authentification utilisateur individuel toohave au lieu d’un service principal.
> 
> 

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority);
    AuthenticationResult authResult = authContext.AcquireTokenAsync("https://management.core.windows.net/",
        clientID, new Uri("http://<redirect URI>"), new PlatformParameters(PromptBehavior.RefreshSession)).Result;

    return authResult;
}
```

Être vraiment tooreplace `<redirect URI>` avec hello rediriger URI que vous avez entré lorsque vous avez inscrit un application hello dans Azure AD.

## <a name="list-cdn-profiles-and-endpoints"></a>Répertorier les profils CDN et points de terminaison
Nous sommes maintenant des opérations de CDN tooperform prêt.  Hello première action notre méthode est la liste de tous les profils de hello et les points de terminaison dans notre groupe de ressources et s’il trouve une correspondance pour les noms de profil et le point de terminaison hello spécifié dans notre constantes, établit que pour une date ultérieure afin de nous n’essayez pas de doublons toocreate.

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all hello CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's hello name of hello CDN profile we want toocreate!
            profileAlreadyExists = true;
        }

        //List all hello CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // hello unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a>Créer des profils CDN et des points de terminaison
Maintenant, nous allons créer un profil.

```csharp
private static void CreateCdnProfile(CdnManagementClient cdn)
{
    if (profileAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating profile {0}.", profileName);
        ProfileCreateParameters profileParms =
            new ProfileCreateParameters() { Location = resourceLocation, Sku = new Sku(SkuName.StandardVerizon) };
        cdn.Profiles.Create(profileName, profileParms, resourceGroupName);
    }
}
```

Une fois le profil de hello est créé, nous allons créer un point de terminaison.

```csharp
private static void CreateCdnEndpoint(CdnManagementClient cdn)
{
    if (endpointAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating endpoint {0} on profile {1}.", endpointName, profileName);
        EndpointCreateParameters endpointParms =
            new EndpointCreateParameters()
            {
                Origins = new List<DeepCreatedOrigin>() { new DeepCreatedOrigin("Contoso", "www.contoso.com") },
                IsHttpAllowed = true,
                IsHttpsAllowed = true,
                Location = resourceLocation
            };
        cdn.Endpoints.Create(endpointName, endpointParms, profileName, resourceGroupName);
    }
}
```

> [!NOTE]
> exemple Hello ci-dessus assigne de point de terminaison hello une origine nommée *Contoso* avec un nom d’hôte `www.contoso.com`.  Vous devez modifier le nom d’hôte toopoint tooyour propre initiale.
> 
> 

## <a name="purge-an-endpoint"></a>Vider un point de terminaison
En supposant que le point de terminaison hello a été créé, une tâche courante que nous souhaitions tooperform dans notre programme purge contenu hello dans notre point de terminaison.

```csharp
private static void PromptPurgeCdnEndpoint(CdnManagementClient cdn)
{
    if (PromptUser(String.Format("Purge CDN endpoint {0}?", endpointName)))
    {
        Console.WriteLine("Purging endpoint. Please wait...");
        cdn.Endpoints.PurgeContent(endpointName, profileName, resourceGroupName, new List<string>() { "/*" });
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

> [!NOTE]
> Dans l’exemple hello ci-dessus, hello chaîne `/*` indique que je veux toopurge tous les éléments racine hello du chemin d’accès du point de terminaison hello.  Cela est équivalent toochecking **purger tous les** Bonjour portail Azure « purge « boîte de dialogue. Bonjour `CreateCdnProfile` (méthode), j’ai créé notre profil comme un **Azure CDN de Verizon** profil à l’aide de code de hello `Sku = new Sku(SkuName.StandardVerizon)`, de sorte que ce sera réussi.  Toutefois, **CDN Azure à partir d’Akamai** profils ne gèrent pas **purger tous les**, donc si j’utilisais un profil Akamai pour ce didacticiel, vous devez tooinclude des chemins d’accès toopurge.
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a>Supprimer des profils CDN et des points de terminaison
méthodes de dernière hello supprimera notre profil et le point de terminaison.

```csharp
private static void PromptDeleteCdnEndpoint(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN endpoint {0} on profile {1}?", endpointName, profileName)))
    {
        Console.WriteLine("Deleting endpoint. Please wait...");
        cdn.Endpoints.DeleteIfExists(endpointName, profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}

private static void PromptDeleteCdnProfile(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN profile {0}?", profileName)))
    {
        Console.WriteLine("Deleting profile. Please wait...");
        cdn.Profiles.DeleteIfExists(profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

## <a name="running-hello-program"></a>Programme hello
Nous pouvons maintenant compiler et exécuter le programme de hello en cliquant sur hello **Démarrer** bouton dans Visual Studio.

![Exécution du programme](./media/cdn-app-dev-net/cdn-program-running-1.png)

Lorsque le programme de hello atteint hello ci-dessus invite, vous devez être en mesure de tooreturn groupe de ressources tooyour Bonjour portail Azure et que le profil de hello a été créé.

![C’est terminé !](./media/cdn-app-dev-net/cdn-success.png)

Nous pouvons ensuite confirmer hello invites toorun hello reste du programme de hello.

![Fin du programme](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a>Étapes suivantes
projet de hello terminée toosee à partir de cette procédure pas à pas, [télécharger l’exemple hello](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).

toofind une documentation supplémentaire sur hello bibliothèque de gestion du CDN Azure pour .NET, hello de vue [référence sur MSDN](https://msdn.microsoft.com/library/mt657769.aspx).

Gérez vos ressources CDN avec [PowerShell](cdn-manage-powershell.md).

