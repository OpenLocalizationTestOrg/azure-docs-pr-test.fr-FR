---
title: "aaaAzure AD v2 Windows Desktop mise en route - le programme d’installation | Documents Microsoft"
description: "Cet article explique comment les applications de bureau Windows .NET (XAML) peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 097ea99bef01e15edaa5ff914ff4e18392b77c5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="479e8-103">Configuration de votre projet</span><span class="sxs-lookup"><span data-stu-id="479e8-103">Set up your project</span></span>

<span data-ttu-id="479e8-104">Cette section fournit des instructions pas à pas toocreate un nouveau toodemonstrate de projet comment toointegrate un bureau Windows .NET Applications (XAML) avec *connectez-vous avec Microsoft* afin qu’il peut interroger les API Web qui requiert un jeton.</span><span class="sxs-lookup"><span data-stu-id="479e8-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="479e8-105">application Hello créée par ce guide expose un bouton toograph et afficher les résultats sur l’écran et un bouton de déconnexion.</span><span class="sxs-lookup"><span data-stu-id="479e8-105">hello application created by this guide exposes a button toograph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="479e8-106">Vous préférez toodownload de projet Visual Studio de cet exemple à la place ?</span><span class="sxs-lookup"><span data-stu-id="479e8-106">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="479e8-107">[Télécharger un projet](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) et ignorer toohello [étape de Configuration](#create-an-application-express) exemple de code hello tooconfigure avant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="479e8-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="479e8-108">Créer votre application</span><span class="sxs-lookup"><span data-stu-id="479e8-108">Create your application</span></span>
1. <span data-ttu-id="479e8-109">Dans Visual Studio : `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="479e8-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="479e8-110">Sous *Modèles*, sélectionnez `Visual C#`</span><span class="sxs-lookup"><span data-stu-id="479e8-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="479e8-111">Sélectionnez `WPF App` (ou *Application WPF* selon la version de hello de votre Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="479e8-111">Select `WPF App` (or *WPF Application* depending on hello version of your Visual Studio)</span></span>

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="479e8-112">Ajouter un projet de tooyour hello bibliothèque d’authentification Microsoft (MSAL)</span><span class="sxs-lookup"><span data-stu-id="479e8-112">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1. <span data-ttu-id="479e8-113">Dans Visual Studio : `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="479e8-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="479e8-114">Copier/coller suivant de hello Bonjour fenêtre de Console du Gestionnaire de Package :</span><span class="sxs-lookup"><span data-stu-id="479e8-114">Copy/paste hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="479e8-115">package Hello ci-dessus installe hello bibliothèque d’authentification Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="479e8-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="479e8-116">MSAL gère l’acquisition, la mise en cache et l’actualisation utilisateur toskens utilisé tooaccess API protégé par Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="479e8-116">MSAL handles acquiring, caching and refreshing user toskens used tooaccess APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-hello-code-tooinitialize-msal"></a><span data-ttu-id="479e8-117">Ajouter le code de hello tooinitialize MSAL</span><span class="sxs-lookup"><span data-stu-id="479e8-117">Add hello code tooinitialize MSAL</span></span>
<span data-ttu-id="479e8-118">Cette étape vous aide à créer une classe toohandle une interaction avec MSAL bibliothèque, telles que la gestion des jetons.</span><span class="sxs-lookup"><span data-stu-id="479e8-118">This step will help you create a class toohandle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="479e8-119">Ouvrez hello `App.xaml.cs` de fichiers et ajouter une référence de hello pour la classe de toohello MSAL bibliothèque :</span><span class="sxs-lookup"><span data-stu-id="479e8-119">Open hello `App.xaml.cs` file and add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="479e8-120">Mise à jour suivante de toohello classe hello application :</span><span class="sxs-lookup"><span data-stu-id="479e8-120">Update hello App class toohello following:</span></span>
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is hello clientId of your app registration. 
    //You have tooreplace hello below with hello Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a><span data-ttu-id="479e8-121">Créer l’interface utilisateur de votre application</span><span class="sxs-lookup"><span data-stu-id="479e8-121">Create your application’s UI</span></span>
<span data-ttu-id="479e8-122">section Hello ci-dessous montre comment une application peut interroger un serveur principal protégé comme Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="479e8-122">hello section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="479e8-123">Un fichier MainWindow.xaml doit être automatiquement créé dans le cadre de votre modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="479e8-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="479e8-124">Ouvrez ce fichier ce fichier et puis suivez les instructions de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="479e8-124">Open this file this file and then follow hello instructions below:</span></span>

<span data-ttu-id="479e8-125">Remplacez votre application `<Grid>` être suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="479e8-125">Replace your application’s `<Grid>` with be hello following:</span></span>

```xml
<Grid>
    <StackPanel Background="Azure">
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
            <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
        </StackPanel>
        <Label Content="API Call Results" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
        <Label Content="Token Info" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
    </StackPanel>
</Grid>
```
