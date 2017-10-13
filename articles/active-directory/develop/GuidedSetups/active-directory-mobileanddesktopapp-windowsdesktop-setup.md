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
## <a name="set-up-your-project"></a>Configuration de votre projet

Cette section fournit des instructions détaillées sur la création d’un nouveau projet pour expliquer comment intégrer une application de bureau Windows .NET (XAML) avec l’option *Se connecter avec Microsoft* pour pouvoir interroger les API web qui requièrent un jeton.

L’application créée par ce guide comprend un bouton pour afficher les résultats à l’écran sous forme graphique, ainsi qu’un bouton de déconnexion.

> Vous préférez télécharger le projet Visual Studio de cet exemple ? [Téléchargez un projet](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) et passez à [l’étape Configuration](#create-an-application-express) pour configurer l’exemple de code avant l’exécution.


### <a name="create-your-application"></a>Créer votre application
1. Dans Visual Studio : `File` > `New` > `Project`<br/>
2. Sous *Modèles*, sélectionnez `Visual C#`
3. Sélectionnez `WPF App` (ou *Application WPF* selon la version de Visual Studio que vous utilisez)

## <a name="add-the-microsoft-authentication-library-msal-to-your-project"></a>Ajoutez Microsoft Authentication Library (MSAL) à votre projet
1. Dans Visual Studio : `Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Copiez et collez la commande suivante dans la fenêtre Console du gestionnaire de package :

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> Le package ci-dessus installe Microsoft Authentication Library (MSAL). MSAL gère l’acquisition, la mise en cache et l’actualisation des jetons d’utilisateur permettant d’accéder aux API protégées par Azure Active Directory v2.

## <a name="add-the-code-to-initialize-msal"></a>Ajoutez le code pour initialiser MSAL
Cette étape vous permet de créer une classe pour gérer l’interaction avec la bibliothèque MSAL, telle que la gestion des jetons.

1. Ouvrez le fichier `App.xaml.cs` et ajoutez la référence de la bibliothèque MSAL à la classe :

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Mettez à jour la classe d’application tel que suit :
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

## <a name="create-your-applications-ui"></a>Créer l’interface utilisateur de votre application
La section suivante explique comment une application peut interroger un serveur principal protégé tel que Microsoft Graph. Un fichier MainWindow.xaml doit être automatiquement créé dans le cadre de votre modèle de projet. Ouvrez ce fichier ce fichier et suivez les instructions ci-dessous :

Remplacez la valeur `<Grid>` de votre application par ce qui suit :

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
