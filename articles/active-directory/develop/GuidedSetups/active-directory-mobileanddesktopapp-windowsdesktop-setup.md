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
## <a name="set-up-your-project"></a>Configuration de votre projet

Cette section fournit des instructions pas à pas toocreate un nouveau toodemonstrate de projet comment toointegrate un bureau Windows .NET Applications (XAML) avec *connectez-vous avec Microsoft* afin qu’il peut interroger les API Web qui requiert un jeton.

application Hello créée par ce guide expose un bouton toograph et afficher les résultats sur l’écran et un bouton de déconnexion.

> Vous préférez toodownload de projet Visual Studio de cet exemple à la place ? [Télécharger un projet](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) et ignorer toohello [étape de Configuration](#create-an-application-express) exemple de code hello tooconfigure avant l’exécution.


### <a name="create-your-application"></a>Créer votre application
1. Dans Visual Studio : `File` > `New` > `Project`<br/>
2. Sous *Modèles*, sélectionnez `Visual C#`
3. Sélectionnez `WPF App` (ou *Application WPF* selon la version de hello de votre Visual Studio)

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a>Ajouter un projet de tooyour hello bibliothèque d’authentification Microsoft (MSAL)
1. Dans Visual Studio : `Tools` > `Nuget Package Manager` > `Package Manager Console`
2. Copier/coller suivant de hello Bonjour fenêtre de Console du Gestionnaire de Package :

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> package Hello ci-dessus installe hello bibliothèque d’authentification Microsoft (MSAL). MSAL gère l’acquisition, la mise en cache et l’actualisation utilisateur toskens utilisé tooaccess API protégé par Azure Active Directory v2.

## <a name="add-hello-code-tooinitialize-msal"></a>Ajouter le code de hello tooinitialize MSAL
Cette étape vous aide à créer une classe toohandle une interaction avec MSAL bibliothèque, telles que la gestion des jetons.

1. Ouvrez hello `App.xaml.cs` de fichiers et ajouter une référence de hello pour la classe de toohello MSAL bibliothèque :

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
Mise à jour suivante de toohello classe hello application :
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

## <a name="create-your-applications-ui"></a>Créer l’interface utilisateur de votre application
section Hello ci-dessous montre comment une application peut interroger un serveur principal protégé comme Microsoft Graph. Un fichier MainWindow.xaml doit être automatiquement créé dans le cadre de votre modèle de projet. Ouvrez ce fichier ce fichier et puis suivez les instructions de hello ci-dessous :

Remplacez votre application `<Grid>` être suivant de hello :

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
