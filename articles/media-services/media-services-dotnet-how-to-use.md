---
title: "aaaHow tooSet installation d’un ordinateur pour le développement de Services de support avec .NET"
description: "En savoir plus sur la configuration requise de hello pour les Services de support à l’aide de hello Media Services SDK pour .NET. Découvrez également comment toocreate une application Visual Studio."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="d2626-104">Développement Media Services avec .NET</span><span class="sxs-lookup"><span data-stu-id="d2626-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="d2626-105">Cette rubrique explique comment les Services de support de développement toostart applications à l’aide de .NET.</span><span class="sxs-lookup"><span data-stu-id="d2626-105">This topic discusses how toostart developing Media Services applications using .NET.</span></span>

<span data-ttu-id="d2626-106">Hello **Azure Media Services .NET SDK** bibliothèque vous permet de tooprogram Media Services à l’aide de .NET.</span><span class="sxs-lookup"><span data-stu-id="d2626-106">hello **Azure Media Services .NET SDK** library enables you tooprogram against Media Services using .NET.</span></span> <span data-ttu-id="d2626-107">toomake elle même toodevelop plus facile avec .NET, hello **Azure Media Services .NET SDK Extensions** bibliothèque est fournie.</span><span class="sxs-lookup"><span data-stu-id="d2626-107">toomake it even easier toodevelop with .NET, hello **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="d2626-108">Cette bibliothèque contient un ensemble de méthodes d’extension et de fonctions d’assistance qui simplifient votre code .NET.</span><span class="sxs-lookup"><span data-stu-id="d2626-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="d2626-109">Les deux bibliothèques sont disponibles par le biais de **NuGet** et de **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="d2626-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2626-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="d2626-110">Prerequisites</span></span>
* <span data-ttu-id="d2626-111">Un compte Media Services dans un abonnement Azure nouveau ou existant.</span><span class="sxs-lookup"><span data-stu-id="d2626-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="d2626-112">Consultez la rubrique de hello [comment tooCreate un compte Media Services](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d2626-112">See hello topic [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="d2626-113">Systèmes d’exploitation : Windows 10, Windows 7, Windows 2008 R2 ou Windows 8.</span><span class="sxs-lookup"><span data-stu-id="d2626-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="d2626-114">.NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="d2626-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="d2626-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2626-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d2626-116">Créer et configurer un projet Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d2626-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="d2626-117">Cette section vous montre comment toocreate un projet dans Visual Studio et le configurer pour un développement Media Services.</span><span class="sxs-lookup"><span data-stu-id="d2626-117">This section shows you how toocreate a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="d2626-118">Dans ce cas, le projet de hello est une application console c# Windows, mais hello mêmes étapes ci-après s’appliquent tooother des types de projets, que vous pouvez créer des applications de Media Services (par exemple, une application Windows Forms ou une application Web ASP.NET).</span><span class="sxs-lookup"><span data-stu-id="d2626-118">In this case, hello project is a C# Windows console application, but hello same setup steps shown here apply tooother types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="d2626-119">Cette section montre comment toouse **NuGet** tooadd Media Services .NET SDK extensions et autres bibliothèques dépendantes.</span><span class="sxs-lookup"><span data-stu-id="d2626-119">This section shows how toouse **NuGet** tooadd Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="d2626-120">Vous pouvez également obtenir les dernières informations Media Services .NET SDK hello à partir de GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) ou [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), générer la solution de hello et ajouter le projet de client toohello hello références.</span><span class="sxs-lookup"><span data-stu-id="d2626-120">Alternatively, you can get hello latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build hello solution, and add hello references toohello client project.</span></span> <span data-ttu-id="d2626-121">Toutes les dépendances nécessaires hello téléchargés et extrait automatiquement.</span><span class="sxs-lookup"><span data-stu-id="d2626-121">All hello necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="d2626-122">Créez une application console C# dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d2626-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="d2626-123">Entrez hello **nom**, **emplacement**, et **nom de la Solution**, puis cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="d2626-123">Enter hello **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="d2626-124">Générez la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="d2626-124">Build hello solution.</span></span>
3. <span data-ttu-id="d2626-125">Utilisez **NuGet** tooinstall et ajoutez **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="d2626-125">Use **NuGet** tooinstall and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="d2626-126">L'installation de ce package installe également le **Kit de développement logiciel (SDK) Media Services pour .NET** et ajoute toutes les autres dépendances requises.</span><span class="sxs-lookup"><span data-stu-id="d2626-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="d2626-127">Assurez-vous que vous avez hello version plus récente de NuGet installée.</span><span class="sxs-lookup"><span data-stu-id="d2626-127">Ensure that you have hello newest version of NuGet installed.</span></span> <span data-ttu-id="d2626-128">Pour obtenir des informations supplémentaires et des instructions relatives à l'installation, consultez la page [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="d2626-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="d2626-129">Dans l’Explorateur de solutions, cliquez sur le nom hello du projet de hello et choisissez Gérer les packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="d2626-129">In Solution Explorer, right-click hello name of hello project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="d2626-130">boîte de dialogue Gérer les Packages NuGet Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d2626-130">hello Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="d2626-131">Dans la galerie en ligne hello, rechercher des Extensions de Windows Azure, choisissez les Extensions de kit de développement .NET Azure Media Services, puis cliquez sur bouton Installer de hello.</span><span class="sxs-lookup"><span data-stu-id="d2626-131">In hello Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click hello Install button.</span></span>
   
    <span data-ttu-id="d2626-132">Hello projet est modifié et fait référence à toohello Extensions Media Services .NET SDK, Media Services .NET SDK, et les autres assemblys dépendants sont ajoutés.</span><span class="sxs-lookup"><span data-stu-id="d2626-132">hello project is modified and references toohello Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="d2626-133">toopromote un environnement de développement plus propre, pensez à activer la restauration des packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="d2626-133">toopromote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="d2626-134">Pour plus d'informations, consultez le document [Restauration du package NuGet](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="d2626-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="d2626-135">Ajoutez une référence trop**System.Configuration** assembly.</span><span class="sxs-lookup"><span data-stu-id="d2626-135">Add a reference too**System.Configuration** assembly.</span></span> <span data-ttu-id="d2626-136">Cet assembly contient hello System.Configuration. **ConfigurationManager** classe qui est utilisé tooaccess des fichiers de configuration (par exemple, App.config).</span><span class="sxs-lookup"><span data-stu-id="d2626-136">This assembly contains hello System.Configuration.**ConfigurationManager** class that is used tooaccess configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="d2626-137">références tooadd à l’aide de la boîte de dialogue Gérer les références hello, cliquez sur le nom de projet de hello Bonjour l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="d2626-137">tooadd references using hello Manage References dialog, right-click hello project name in hello Solution Explorer.</span></span> <span data-ttu-id="d2626-138">Sélectionnez ensuite Ajouter et Références.</span><span class="sxs-lookup"><span data-stu-id="d2626-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="d2626-139">boîte de dialogue Gérer les références Hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d2626-139">hello Manage References dialog appears.</span></span>
8. <span data-ttu-id="d2626-140">Sous les assemblys .NET framework, rechercher et sélectionnez l’assembly System.Configuration hello et appuyez sur OK.</span><span class="sxs-lookup"><span data-stu-id="d2626-140">Under .NET framework assemblies, find and select hello System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="d2626-141">Ouvrez le fichier App.config de hello et ajoutez un *appSettings* toohello section du fichier.</span><span class="sxs-lookup"><span data-stu-id="d2626-141">Open hello App.config file and add an *appSettings* section toohello file.</span></span>     
   
    <span data-ttu-id="d2626-142">Définir les valeurs hello qui sont nécessaires tooconnect toohello API Media Services.</span><span class="sxs-lookup"><span data-stu-id="d2626-142">Set hello values that are needed tooconnect toohello Media Services API.</span></span> <span data-ttu-id="d2626-143">Pour plus d’informations, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d2626-143">For more information, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="d2626-144">Si vous utilisez [l’authentification utilisateur](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) votre fichier de configuration sera probablement ont des valeurs pour votre domaine de locataire Azure AD et hello du point de terminaison AMS REST API.</span><span class="sxs-lookup"><span data-stu-id="d2626-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and hello AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="d2626-145">La plupart des exemples de code Bonjour documentation Azure Media Services définie, utilisez un type (interactif) d’utilisateur de l’authentification tooconnect toohello AMS API.</span><span class="sxs-lookup"><span data-stu-id="d2626-145">Most code samples in hello Azure Media Services documentation set, use a user (interactive) type of authentication tooconnect toohello AMS API.</span></span> <span data-ttu-id="d2626-146">Cette méthode d’authentification fonctionne bien avec les applications natives de gestion ou de surveillance : applications mobiles, applications Windows et applications de console.</span><span class="sxs-lookup"><span data-stu-id="d2626-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="d2626-147">Cette méthode d’authentification ne convient pas aux applications de type serveur, services web et API.</span><span class="sxs-lookup"><span data-stu-id="d2626-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="d2626-148">Pour plus d’informations, consultez [hello accès AMS API avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="d2626-148">For more information, see [Access hello AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="d2626-149">Remplacer hello existants **à l’aide de** instructions au début de hello du fichier Program.cs de hello avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="d2626-149">Overwrite hello existing **using** statements at hello beginning of hello Program.cs file with hello following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="d2626-150">À ce stade, vous êtes prêt toostart développe une application de Media Services.</span><span class="sxs-lookup"><span data-stu-id="d2626-150">At this point, you are ready toostart developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="d2626-151">Exemple</span><span class="sxs-lookup"><span data-stu-id="d2626-151">Example</span></span>

<span data-ttu-id="d2626-152">Voici un exemple de petit qui se connecte toohello AMS API et répertorie tous les processeurs multimédias disponibles.</span><span class="sxs-lookup"><span data-stu-id="d2626-152">Here is a small example that connects toohello AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a><span data-ttu-id="d2626-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d2626-153">Next steps</span></span>

<span data-ttu-id="d2626-154">Maintenant [vous pouvez vous connecter toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) et démarrer [développement](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d2626-154">Now [you can connect toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="d2626-155">Parcours d’apprentissage de Media Services</span><span class="sxs-lookup"><span data-stu-id="d2626-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d2626-156">Fournir des commentaires</span><span class="sxs-lookup"><span data-stu-id="d2626-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

