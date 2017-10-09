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
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="d3e69-103">Prise en main du développement Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d3e69-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3e69-104">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d3e69-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="d3e69-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d3e69-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="d3e69-106">Vous pouvez utiliser hello [bibliothèque du CDN Azure pour .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate création et la gestion des profils CDN et des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d3e69-106">You can use hello [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="d3e69-107">Ce didacticiel guide dans la création d’une application console .NET simple qui illustre plusieurs opérations disponibles de hello hello.</span><span class="sxs-lookup"><span data-stu-id="d3e69-107">This tutorial walks through hello creation of a simple .NET console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="d3e69-108">Ce didacticiel n’est pas conçu toodescribe tous les aspects de hello Azure CDN bibliothèque pour .NET en détail.</span><span class="sxs-lookup"><span data-stu-id="d3e69-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="d3e69-109">Vous avez besoin de Visual Studio 2015 toocomplete ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d3e69-109">You need Visual Studio 2015 toocomplete this tutorial.</span></span>  <span data-ttu-id="d3e69-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) est disponible gratuitement en téléchargement.</span><span class="sxs-lookup"><span data-stu-id="d3e69-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="d3e69-111">Hello [projet achevé de ce didacticiel](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) est disponible pour téléchargement sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="d3e69-111">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="d3e69-112">Créer votre projet et ajouter des packages Nuget</span><span class="sxs-lookup"><span data-stu-id="d3e69-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="d3e69-113">Maintenant que nous avons créé un groupe de ressources pour les profils de notre CDN et donné notre profils CDN toomanage d’autorisation d’application Azure AD et les points de terminaison de ce groupe, nous pouvons commencer à créer notre application.</span><span class="sxs-lookup"><span data-stu-id="d3e69-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="d3e69-114">Dans Visual Studio 2015, cliquez sur **fichier**, **nouveau**, **projet...**  tooopen hello nouvelle boîte de dialogue projet.</span><span class="sxs-lookup"><span data-stu-id="d3e69-114">From within Visual Studio 2015, click **File**, **New**, **Project...** tooopen hello new project dialog.</span></span>  <span data-ttu-id="d3e69-115">Développez **Visual C#**, puis sélectionnez **Windows** dans le volet gauche de hello hello.</span><span class="sxs-lookup"><span data-stu-id="d3e69-115">Expand **Visual C#**, then select **Windows** in hello pane on hello left.</span></span>  <span data-ttu-id="d3e69-116">Cliquez sur **Application Console** dans le volet central de hello.</span><span class="sxs-lookup"><span data-stu-id="d3e69-116">Click **Console Application** in hello center pane.</span></span>  <span data-ttu-id="d3e69-117">Nommez votre projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d3e69-117">Name your project, then click **OK**.</span></span>  

![Nouveau projet](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="d3e69-119">Notre projet va toouse certaines bibliothèques Azure contenues dans les packages Nuget.</span><span class="sxs-lookup"><span data-stu-id="d3e69-119">Our project is going toouse some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="d3e69-120">Vous allez ajouter ces projets toohello.</span><span class="sxs-lookup"><span data-stu-id="d3e69-120">Let's add those toohello project.</span></span>

1. <span data-ttu-id="d3e69-121">Cliquez sur hello **outils** menu, **Gestionnaire de Package Nuget**, puis **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="d3e69-121">Click hello **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Gérer les packages NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="d3e69-123">Dans la Console du Gestionnaire de Package de hello, exécutez hello suivant commande tooinstall hello **Active Directory Authentication Library (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="d3e69-123">In hello Package Manager Console, execute hello following command tooinstall hello **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="d3e69-124">Exécutez hello suivant tooinstall hello **bibliothèque de gestion Azure CDN**:</span><span class="sxs-lookup"><span data-stu-id="d3e69-124">Execute hello following tooinstall hello **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="d3e69-125">Directives, constantes, méthode principale et méthodes d’assistance</span><span class="sxs-lookup"><span data-stu-id="d3e69-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="d3e69-126">Passons la structure de base hello de notre programme écrit.</span><span class="sxs-lookup"><span data-stu-id="d3e69-126">Let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="d3e69-127">Dans l’onglet de Program.cs hello, remplacez hello `using` directives haut hello, avec les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="d3e69-127">Back in hello Program.cs tab, replace hello `using` directives at hello top with hello following:</span></span>
   
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
2. <span data-ttu-id="d3e69-128">Nous devons toodefine certaines constantes que nos méthodes utilisera.</span><span class="sxs-lookup"><span data-stu-id="d3e69-128">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="d3e69-129">Bonjour `Program` (classe), mais avant l’exécution hello `Main` méthode, ajoutez hello qui suit.</span><span class="sxs-lookup"><span data-stu-id="d3e69-129">In hello `Program` class, but before hello `Main` method, add hello following.</span></span>  <span data-ttu-id="d3e69-130">Être tooreplace que des espaces réservés de hello, y compris hello  **&lt;crochets pointus&gt;**, avec vos propres valeurs en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="d3e69-130">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="d3e69-131">Également au niveau de classe hello, vous devez définir ces deux variables.</span><span class="sxs-lookup"><span data-stu-id="d3e69-131">Also at hello class level, define these two variables.</span></span>  <span data-ttu-id="d3e69-132">Nous allons utiliser ces toodetermine ultérieure si notre profil et le point de terminaison existent déjà.</span><span class="sxs-lookup"><span data-stu-id="d3e69-132">We'll use these later toodetermine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="d3e69-133">Remplacez hello `Main` méthode comme suit :</span><span class="sxs-lookup"><span data-stu-id="d3e69-133">Replace hello `Main` method as follows:</span></span>
   
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
5. <span data-ttu-id="d3e69-134">Certaines de nos autres méthodes vont utilisateur de hello tooprompt des questions de « Oui/non ».</span><span class="sxs-lookup"><span data-stu-id="d3e69-134">Some of our other methods are going tooprompt hello user with "Yes/No" questions.</span></span>  <span data-ttu-id="d3e69-135">Ajouter hello suivant de méthode toomake qui un peu plus simple :</span><span class="sxs-lookup"><span data-stu-id="d3e69-135">Add hello following method toomake that a little easier:</span></span>
   
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

<span data-ttu-id="d3e69-136">Maintenant que la structure de base hello de notre programme est écrit, nous devons créer des méthodes de hello appelées par hello `Main` (méthode).</span><span class="sxs-lookup"><span data-stu-id="d3e69-136">Now that hello basic structure of our program is written, we should create hello methods called by hello `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="d3e69-137">Authentification</span><span class="sxs-lookup"><span data-stu-id="d3e69-137">Authentication</span></span>
<span data-ttu-id="d3e69-138">Avant de pouvoir utiliser hello bibliothèque de gestion Azure CDN, vous avez besoin tooauthenticate notre service principal et obtenir un jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="d3e69-138">Before we can use hello Azure CDN Management Library, we need tooauthenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="d3e69-139">Cette méthode utilise le jeton de hello tooretrieve ADAL.</span><span class="sxs-lookup"><span data-stu-id="d3e69-139">This method uses ADAL tooretrieve hello token.</span></span>

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

<span data-ttu-id="d3e69-140">Si vous utilisez l’authentification des utilisateurs individuels, hello `GetAccessToken` méthode aura un aspect légèrement différente.</span><span class="sxs-lookup"><span data-stu-id="d3e69-140">If you are using individual user authentication, hello `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d3e69-141">Utilisez uniquement cet exemple de code si vous choisissez l’authentification utilisateur individuel toohave au lieu d’un service principal.</span><span class="sxs-lookup"><span data-stu-id="d3e69-141">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="d3e69-142">Être vraiment tooreplace `<redirect URI>` avec hello rediriger URI que vous avez entré lorsque vous avez inscrit un application hello dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3e69-142">Be sure tooreplace `<redirect URI>` with hello redirect URI you entered when you registered hello application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="d3e69-143">Répertorier les profils CDN et points de terminaison</span><span class="sxs-lookup"><span data-stu-id="d3e69-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="d3e69-144">Nous sommes maintenant des opérations de CDN tooperform prêt.</span><span class="sxs-lookup"><span data-stu-id="d3e69-144">Now we're ready tooperform CDN operations.</span></span>  <span data-ttu-id="d3e69-145">Hello première action notre méthode est la liste de tous les profils de hello et les points de terminaison dans notre groupe de ressources et s’il trouve une correspondance pour les noms de profil et le point de terminaison hello spécifié dans notre constantes, établit que pour une date ultérieure afin de nous n’essayez pas de doublons toocreate.</span><span class="sxs-lookup"><span data-stu-id="d3e69-145">hello first thing our method does is list all hello profiles and endpoints in our resource group, and if it finds a match for hello profile and endpoint names specified in our constants, makes a note of that for later so we don't try toocreate duplicates.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="d3e69-146">Créer des profils CDN et des points de terminaison</span><span class="sxs-lookup"><span data-stu-id="d3e69-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="d3e69-147">Maintenant, nous allons créer un profil.</span><span class="sxs-lookup"><span data-stu-id="d3e69-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="d3e69-148">Une fois le profil de hello est créé, nous allons créer un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d3e69-148">Once hello profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="d3e69-149">exemple Hello ci-dessus assigne de point de terminaison hello une origine nommée *Contoso* avec un nom d’hôte `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="d3e69-149">hello example above assigns hello endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="d3e69-150">Vous devez modifier le nom d’hôte toopoint tooyour propre initiale.</span><span class="sxs-lookup"><span data-stu-id="d3e69-150">You should change this toopoint tooyour own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="d3e69-151">Vider un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="d3e69-151">Purge an endpoint</span></span>
<span data-ttu-id="d3e69-152">En supposant que le point de terminaison hello a été créé, une tâche courante que nous souhaitions tooperform dans notre programme purge contenu hello dans notre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d3e69-152">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging hello content in our endpoint.</span></span>

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
> <span data-ttu-id="d3e69-153">Dans l’exemple hello ci-dessus, hello chaîne `/*` indique que je veux toopurge tous les éléments racine hello du chemin d’accès du point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="d3e69-153">In hello example above, hello string `/*` denotes that I want toopurge everything in hello root of hello endpoint path.</span></span>  <span data-ttu-id="d3e69-154">Cela est équivalent toochecking **purger tous les** Bonjour portail Azure « purge « boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="d3e69-154">This is equivalent toochecking **Purge All** in hello Azure portal's "purge" dialog.</span></span> <span data-ttu-id="d3e69-155">Bonjour `CreateCdnProfile` (méthode), j’ai créé notre profil comme un **Azure CDN de Verizon** profil à l’aide de code de hello `Sku = new Sku(SkuName.StandardVerizon)`, de sorte que ce sera réussi.</span><span class="sxs-lookup"><span data-stu-id="d3e69-155">In hello `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using hello code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="d3e69-156">Toutefois, **CDN Azure à partir d’Akamai** profils ne gèrent pas **purger tous les**, donc si j’utilisais un profil Akamai pour ce didacticiel, vous devez tooinclude des chemins d’accès toopurge.</span><span class="sxs-lookup"><span data-stu-id="d3e69-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need tooinclude specific paths toopurge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="d3e69-157">Supprimer des profils CDN et des points de terminaison</span><span class="sxs-lookup"><span data-stu-id="d3e69-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="d3e69-158">méthodes de dernière hello supprimera notre profil et le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d3e69-158">hello last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="d3e69-159">Programme hello</span><span class="sxs-lookup"><span data-stu-id="d3e69-159">Running hello program</span></span>
<span data-ttu-id="d3e69-160">Nous pouvons maintenant compiler et exécuter le programme de hello en cliquant sur hello **Démarrer** bouton dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d3e69-160">We can now compile and run hello program by clicking hello **Start** button in Visual Studio.</span></span>

![Exécution du programme](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="d3e69-162">Lorsque le programme de hello atteint hello ci-dessus invite, vous devez être en mesure de tooreturn groupe de ressources tooyour Bonjour portail Azure et que le profil de hello a été créé.</span><span class="sxs-lookup"><span data-stu-id="d3e69-162">When hello program reaches hello above prompt, you should be able tooreturn tooyour resource group in hello Azure portal and see that hello profile has been created.</span></span>

![C’est terminé !](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="d3e69-164">Nous pouvons ensuite confirmer hello invites toorun hello reste du programme de hello.</span><span class="sxs-lookup"><span data-stu-id="d3e69-164">We can then confirm hello prompts toorun hello rest of hello program.</span></span>

![Fin du programme](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="d3e69-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d3e69-166">Next Steps</span></span>
<span data-ttu-id="d3e69-167">projet de hello terminée toosee à partir de cette procédure pas à pas, [télécharger l’exemple hello](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="d3e69-167">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="d3e69-168">toofind une documentation supplémentaire sur hello bibliothèque de gestion du CDN Azure pour .NET, hello de vue [référence sur MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="d3e69-168">toofind additional documentation on hello Azure CDN Management Library for .NET, view hello [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="d3e69-169">Gérez vos ressources CDN avec [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d3e69-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

