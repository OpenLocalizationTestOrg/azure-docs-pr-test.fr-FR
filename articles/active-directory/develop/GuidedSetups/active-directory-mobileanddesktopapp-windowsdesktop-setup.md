---
title: "Prise en main d’Azure AD v2 avec les applications de bureau Windows - Paramétrage | Microsoft Docs"
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
ms.openlocfilehash: 4065727aef04d7969d438c6ef79127bb44568be1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="984dd-103">Configuration de votre projet</span><span class="sxs-lookup"><span data-stu-id="984dd-103">Set up your project</span></span>

<span data-ttu-id="984dd-104">Cette section fournit des instructions détaillées sur la création d’un nouveau projet pour expliquer comment intégrer une application de bureau Windows .NET (XAML) avec l’option *Se connecter avec Microsoft* pour pouvoir interroger les API web qui requièrent un jeton.</span><span class="sxs-lookup"><span data-stu-id="984dd-104">This section provides step-by-step instructions for how to create a new project to demonstrate how to integrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="984dd-105">L’application créée par ce guide comprend un bouton pour afficher les résultats à l’écran sous forme graphique, ainsi qu’un bouton de déconnexion.</span><span class="sxs-lookup"><span data-stu-id="984dd-105">The application created by this guide exposes a button to graph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="984dd-106">Vous préférez télécharger le projet Visual Studio de cet exemple ?</span><span class="sxs-lookup"><span data-stu-id="984dd-106">Prefer to download this sample's Visual Studio project instead?</span></span> <span data-ttu-id="984dd-107">[Téléchargez un projet](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) et passez à [l’étape Configuration](#create-an-application-express) pour configurer l’exemple de code avant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="984dd-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip to the [Configuration step](#create-an-application-express) to configure the code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="984dd-108">Créer votre application</span><span class="sxs-lookup"><span data-stu-id="984dd-108">Create your application</span></span>
1. <span data-ttu-id="984dd-109">Dans Visual Studio : `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="984dd-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="984dd-110">Sous *Modèles*, sélectionnez `Visual C#`</span><span class="sxs-lookup"><span data-stu-id="984dd-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="984dd-111">Sélectionnez `WPF App` (ou *Application WPF* selon la version de Visual Studio que vous utilisez)</span><span class="sxs-lookup"><span data-stu-id="984dd-111">Select `WPF App` (or *WPF Application* depending on the version of your Visual Studio)</span></span>

## <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a><span data-ttu-id="984dd-112">Ajoutez Microsoft Authentication Library (MSAL) à votre projet</span><span class="sxs-lookup"><span data-stu-id="984dd-112">Add the Microsoft Authentication Library (MSAL) to your project</span></span>
1. <span data-ttu-id="984dd-113">Dans Visual Studio : `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="984dd-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="984dd-114">Copiez et collez la commande suivante dans la fenêtre Console du gestionnaire de package :</span><span class="sxs-lookup"><span data-stu-id="984dd-114">Copy/paste the following in the Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="984dd-115">Le package ci-dessus installe Microsoft Authentication Library (MSAL).</span><span class="sxs-lookup"><span data-stu-id="984dd-115">The package above installs the Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="984dd-116">MSAL gère l’acquisition, la mise en cache et l’actualisation des jetons d’utilisateur permettant d’accéder aux API protégées par Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="984dd-116">MSAL handles acquiring, caching and refreshing user toskens used to access APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-the-code-to-initialize-msal"></a><span data-ttu-id="984dd-117">Ajoutez le code pour initialiser MSAL</span><span class="sxs-lookup"><span data-stu-id="984dd-117">Add the code to initialize MSAL</span></span>
<span data-ttu-id="984dd-118">Cette étape vous permet de créer une classe pour gérer l’interaction avec la bibliothèque MSAL, telle que la gestion des jetons.</span><span class="sxs-lookup"><span data-stu-id="984dd-118">This step will help you create a class to handle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="984dd-119">Ouvrez le fichier `App.xaml.cs` et ajoutez la référence de la bibliothèque MSAL à la classe :</span><span class="sxs-lookup"><span data-stu-id="984dd-119">Open the `App.xaml.cs` file and add the reference for MSAL library to the class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="984dd-120">Mettez à jour la classe d’application tel que suit :</span><span class="sxs-lookup"><span data-stu-id="984dd-120">Update the App class to the following:</span></span>
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is the clientId of your app registration. 
    //You have to replace the below with the Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a><span data-ttu-id="984dd-121">Créer l’interface utilisateur de votre application</span><span class="sxs-lookup"><span data-stu-id="984dd-121">Create your application’s UI</span></span>
<span data-ttu-id="984dd-122">La section suivante explique comment une application peut interroger un serveur principal protégé tel que Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="984dd-122">The section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="984dd-123">Un fichier MainWindow.xaml doit être automatiquement créé dans le cadre de votre modèle de projet.</span><span class="sxs-lookup"><span data-stu-id="984dd-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="984dd-124">Ouvrez ce fichier ce fichier et suivez les instructions ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="984dd-124">Open this file this file and then follow the instructions below:</span></span>

<span data-ttu-id="984dd-125">Remplacez la valeur `<Grid>` de votre application par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="984dd-125">Replace your application’s `<Grid>` with be the following:</span></span>

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
