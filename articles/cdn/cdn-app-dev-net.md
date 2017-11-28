---
title: "Prise en main de la bibliothèque Azure CDN pour .NET | Microsoft Docs"
description: "Apprenez à écrire des applications .NET pour gérer Azure CDN à l’aide de Visual Studio."
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
ms.openlocfilehash: 5379586355ece98af6295236d6cbd09cb31c742b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="d8c0c-103">Prise en main du développement Azure CDN</span><span class="sxs-lookup"><span data-stu-id="d8c0c-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d8c0c-104">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d8c0c-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="d8c0c-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d8c0c-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="d8c0c-106">Vous pouvez utiliser la [bibliothèque Azure CDN pour .NET](https://msdn.microsoft.com/library/mt657769.aspx) pour automatiser la création et la gestion des points de terminaison et profils CDN.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-106">You can use the [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="d8c0c-107">Ce didacticiel présente la création d’une application console .NET simple, qui exécute plusieurs des opérations disponibles.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-107">This tutorial walks through the creation of a simple .NET console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="d8c0c-108">Il n’a pas vocation à décrire en détail tous les aspects de la bibliothèque Azure CDN pour .NET.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-108">This tutorial is not intended to describe all aspects of the Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="d8c0c-109">Pour suivre ce didacticiel, vous avez besoin de Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-109">You need Visual Studio 2015 to complete this tutorial.</span></span>  <span data-ttu-id="d8c0c-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) est disponible gratuitement en téléchargement.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="d8c0c-111">Le [projet achevé de ce didacticiel](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) est disponible en téléchargement sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-111">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="d8c0c-112">Créer votre projet et ajouter des packages Nuget</span><span class="sxs-lookup"><span data-stu-id="d8c0c-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="d8c0c-113">Maintenant que nous avons créé un groupe de ressources pour nos profils CDN et autorisé l’application Azure AD à gérer les points de terminaison et profils CDN au sein de ce groupe, nous pouvons créer notre application.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="d8c0c-114">Dans Visual Studio 2015, cliquez sur **Fichier**, **Nouveau**, **Projet...** pour ouvrir la boîte de dialogue Nouveau projet.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-114">From within Visual Studio 2015, click **File**, **New**, **Project...** to open the new project dialog.</span></span>  <span data-ttu-id="d8c0c-115">Développez **Visual C#**, puis sélectionnez **Windows** dans le volet de gauche.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-115">Expand **Visual C#**, then select **Windows** in the pane on the left.</span></span>  <span data-ttu-id="d8c0c-116">Cliquez sur **Application console** dans le volet central.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-116">Click **Console Application** in the center pane.</span></span>  <span data-ttu-id="d8c0c-117">Nommez votre projet, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-117">Name your project, then click **OK**.</span></span>  

![Nouveau projet](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="d8c0c-119">Notre projet va utiliser certaines bibliothèques Azure contenues dans des packages Nuget.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-119">Our project is going to use some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="d8c0c-120">Ajoutons-les à ce projet.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-120">Let's add those to the project.</span></span>

1. <span data-ttu-id="d8c0c-121">Dans le menu **Outils**, sélectionnez **Gestionnaire de package NuGet**, puis **Console du Gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-121">Click the **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Gérer les packages NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="d8c0c-123">Dans la Console du Gestionnaire de package, exécutez la commande suivante pour installer la bibliothèque **ADAL (Active Directory Authentication Library)**:</span><span class="sxs-lookup"><span data-stu-id="d8c0c-123">In the Package Manager Console, execute the following command to install the **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="d8c0c-124">Exécutez la commande suivante pour installer la bibliothèque **Azure CDN Management Library**:</span><span class="sxs-lookup"><span data-stu-id="d8c0c-124">Execute the following to install the **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="d8c0c-125">Directives, constantes, méthode principale et méthodes d’assistance</span><span class="sxs-lookup"><span data-stu-id="d8c0c-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="d8c0c-126">Rédigeons la structure de base de notre programme.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-126">Let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="d8c0c-127">Dans l’onglet Program.cs, remplacez les directives `using` au début par les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="d8c0c-127">Back in the Program.cs tab, replace the `using` directives at the top with the following:</span></span>
   
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
2. <span data-ttu-id="d8c0c-128">Nous devons définir certaines constantes que nos méthodes utiliseront.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-128">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="d8c0c-129">Dans la classe `Program` mais avant la méthode `Main`, ajoutez le code suivant.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-129">In the `Program` class, but before the `Main` method, add the following.</span></span>  <span data-ttu-id="d8c0c-130">Veillez à remplacer les espaces réservés, y compris les **&lt;éléments entre chevrons&gt;**, par vos propres valeurs, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-130">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="d8c0c-131">De plus, au niveau de la classe, vous devez définir ces deux variables.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-131">Also at the class level, define these two variables.</span></span>  <span data-ttu-id="d8c0c-132">Nous les utiliserons ultérieurement pour déterminer si notre profil et notre point de terminaison existent déjà.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-132">We'll use these later to determine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="d8c0c-133">Remplacez la méthode `Main` comme suit :</span><span class="sxs-lookup"><span data-stu-id="d8c0c-133">Replace the `Main` method as follows:</span></span>
   
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
   
       Console.WriteLine("Press Enter to end program.");
       Console.ReadLine();
   }
   ```
5. <span data-ttu-id="d8c0c-134">Certaines de nos autres méthodes posent à l’utilisateur des questions fermées (de type Oui/non).</span><span class="sxs-lookup"><span data-stu-id="d8c0c-134">Some of our other methods are going to prompt the user with "Yes/No" questions.</span></span>  <span data-ttu-id="d8c0c-135">Ajoutez la méthode suivante pour faciliter l’opération :</span><span class="sxs-lookup"><span data-stu-id="d8c0c-135">Add the following method to make that a little easier:</span></span>
   
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

<span data-ttu-id="d8c0c-136">Maintenant que la structure de base de notre programme est écrite, nous devons créer les méthodes appelées par la méthode `Main` .</span><span class="sxs-lookup"><span data-stu-id="d8c0c-136">Now that the basic structure of our program is written, we should create the methods called by the `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="d8c0c-137">Authentification</span><span class="sxs-lookup"><span data-stu-id="d8c0c-137">Authentication</span></span>
<span data-ttu-id="d8c0c-138">Pour pouvoir utiliser la bibliothèque Azure CDN Management Library, nous devons authentifier notre principal de service et obtenir un jeton d’authentification.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-138">Before we can use the Azure CDN Management Library, we need to authenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="d8c0c-139">Cette méthode utilise la bibliothèque ADAL pour récupérer le jeton.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-139">This method uses ADAL to retrieve the token.</span></span>

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

<span data-ttu-id="d8c0c-140">Si vous utilisez l’authentification d’utilisateurs individuels, la méthode `GetAccessToken` se présentera légèrement différemment.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-140">If you are using individual user authentication, the `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8c0c-141">N’utilisez ce code que si vous privilégiez l’authentification d’utilisateurs individuels au principal du service.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-141">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="d8c0c-142">Veillez à remplacer `<redirect URI>` par l’URI de redirection que vous avez saisie lors de l’inscription de l’application dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-142">Be sure to replace `<redirect URI>` with the redirect URI you entered when you registered the application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="d8c0c-143">Répertorier les profils CDN et points de terminaison</span><span class="sxs-lookup"><span data-stu-id="d8c0c-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="d8c0c-144">Nous sommes maintenant prêts à effectuer des opérations CDN.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-144">Now we're ready to perform CDN operations.</span></span>  <span data-ttu-id="d8c0c-145">La première action de notre méthode est de répertorier tous les profils et points de terminaison dans notre groupe de ressources. Si elle trouve une correspondance avec les noms de profil et de point de terminaison spécifiés dans nos constantes, elle la mémorise pour éviter de créer des doublons.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-145">The first thing our method does is list all the profiles and endpoints in our resource group, and if it finds a match for the profile and endpoint names specified in our constants, makes a note of that for later so we don't try to create duplicates.</span></span>

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all the CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's the name of the CDN profile we want to create!
            profileAlreadyExists = true;
        }

        //List all the CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // The unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="d8c0c-146">Créer des profils CDN et des points de terminaison</span><span class="sxs-lookup"><span data-stu-id="d8c0c-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="d8c0c-147">Maintenant, nous allons créer un profil.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="d8c0c-148">Après le profil, nous allons créer un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-148">Once the profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="d8c0c-149">L’exemple ci-dessus attribue au point de terminaison une origine nommée *Contoso* avec un nom d’hôte `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-149">The example above assigns the endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="d8c0c-150">Vous devez remplacer celui-ci par le nom d’hôte de votre propre origine.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-150">You should change this to point to your own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="d8c0c-151">Vider un point de terminaison</span><span class="sxs-lookup"><span data-stu-id="d8c0c-151">Purge an endpoint</span></span>
<span data-ttu-id="d8c0c-152">En supposant que le point de terminaison a été créé, une tâche courante que nous pouvons effectuer dans notre programme consiste à vider le contenu de notre point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-152">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging the content in our endpoint.</span></span>

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
> <span data-ttu-id="d8c0c-153">Dans l’exemple ci-dessus, la chaîne `/*` indique que je souhaite vider tous les éléments à la racine du chemin d’accès du point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-153">In the example above, the string `/*` denotes that I want to purge everything in the root of the endpoint path.</span></span>  <span data-ttu-id="d8c0c-154">Cela revient à cocher la case **Purge All** (Purger tout) dans la boîte de dialogue de vidage du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-154">This is equivalent to checking **Purge All** in the Azure portal's "purge" dialog.</span></span> <span data-ttu-id="d8c0c-155">Dans la méthode `CreateCdnProfile`, j’ai créé notre profil comme un profil **Azure CDN de Verizon** à l’aide du code `Sku = new Sku(SkuName.StandardVerizon)`, pour que l’opération aboutisse.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-155">In the `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using the code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="d8c0c-156">Toutefois, les profils **Azure CDN de Akamai** ne prennent pas en charge l’option **Purge All** (Purger tout). Donc, si j’utilisais un profil Akamai pour ce didacticiel, je devrais inclure les chemins d’accès spécifiques à vider.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need to include specific paths to purge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="d8c0c-157">Supprimer des profils CDN et des points de terminaison</span><span class="sxs-lookup"><span data-stu-id="d8c0c-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="d8c0c-158">Les dernières méthodes supprimeront notre point de terminaison et notre profil.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-158">The last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-the-program"></a><span data-ttu-id="d8c0c-159">Exécution du programme</span><span class="sxs-lookup"><span data-stu-id="d8c0c-159">Running the program</span></span>
<span data-ttu-id="d8c0c-160">Nous pouvons maintenant compiler et exécuter le programme en cliquant sur le bouton **Démarrer** dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-160">We can now compile and run the program by clicking the **Start** button in Visual Studio.</span></span>

![Exécution du programme](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="d8c0c-162">Lorsque le programme atteint l’invite ci-dessus, vous pouvez revenir à votre groupe de ressources dans le portail Azure et vérifier que le profil a été créé.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-162">When the program reaches the above prompt, you should be able to return to your resource group in the Azure portal and see that the profile has been created.</span></span>

![Vous avez réussi !](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="d8c0c-164">Nous pouvons alors confirmer les invites pour exécuter le reste du programme.</span><span class="sxs-lookup"><span data-stu-id="d8c0c-164">We can then confirm the prompts to run the rest of the program.</span></span>

![Fin du programme](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="d8c0c-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d8c0c-166">Next Steps</span></span>
<span data-ttu-id="d8c0c-167">Pour voir le projet achevé obtenu à partir de cette procédure pas à pas, [téléchargez l’exemple](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="d8c0c-167">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="d8c0c-168">Pour trouver de la documentation supplémentaire sur la bibliothèque Azure CDN Management Library pour .NET, consultez la [référence sur MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8c0c-168">To find additional documentation on the Azure CDN Management Library for .NET, view the [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="d8c0c-169">Gérez vos ressources CDN avec [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d8c0c-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

