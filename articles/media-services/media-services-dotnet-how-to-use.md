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
# <a name="media-services-development-with-net"></a>Développement Media Services avec .NET
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Cette rubrique explique comment les Services de support de développement toostart applications à l’aide de .NET.

Hello **Azure Media Services .NET SDK** bibliothèque vous permet de tooprogram Media Services à l’aide de .NET. toomake elle même toodevelop plus facile avec .NET, hello **Azure Media Services .NET SDK Extensions** bibliothèque est fournie. Cette bibliothèque contient un ensemble de méthodes d’extension et de fonctions d’assistance qui simplifient votre code .NET. Les deux bibliothèques sont disponibles par le biais de **NuGet** et de **GitHub**.

## <a name="prerequisites"></a>Conditions préalables
* Un compte Media Services dans un abonnement Azure nouveau ou existant. Consultez la rubrique de hello [comment tooCreate un compte Media Services](media-services-portal-create-account.md).
* Systèmes d’exploitation : Windows 10, Windows 7, Windows 2008 R2 ou Windows 8.
* .NET Framework 4.5.
* Visual Studio.

## <a name="create-and-configure-a-visual-studio-project"></a>Créer et configurer un projet Visual Studio
Cette section vous montre comment toocreate un projet dans Visual Studio et le configurer pour un développement Media Services.  Dans ce cas, le projet de hello est une application console c# Windows, mais hello mêmes étapes ci-après s’appliquent tooother des types de projets, que vous pouvez créer des applications de Media Services (par exemple, une application Windows Forms ou une application Web ASP.NET).

Cette section montre comment toouse **NuGet** tooadd Media Services .NET SDK extensions et autres bibliothèques dépendantes.

Vous pouvez également obtenir les dernières informations Media Services .NET SDK hello à partir de GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) ou [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), générer la solution de hello et ajouter le projet de client toohello hello références. Toutes les dépendances nécessaires hello téléchargés et extrait automatiquement.

1. Créez une application console C# dans Visual Studio. Entrez hello **nom**, **emplacement**, et **nom de la Solution**, puis cliquez sur OK.
2. Générez la solution de hello.
3. Utilisez **NuGet** tooinstall et ajoutez **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**). L'installation de ce package installe également le **Kit de développement logiciel (SDK) Media Services pour .NET** et ajoute toutes les autres dépendances requises.
   
    Assurez-vous que vous avez hello version plus récente de NuGet installée. Pour obtenir des informations supplémentaires et des instructions relatives à l'installation, consultez la page [NuGet](http://nuget.codeplex.com/).
4. Dans l’Explorateur de solutions, cliquez sur le nom hello du projet de hello et choisissez Gérer les packages NuGet.
   
    boîte de dialogue Gérer les Packages NuGet Hello s’affiche.
5. Dans la galerie en ligne hello, rechercher des Extensions de Windows Azure, choisissez les Extensions de kit de développement .NET Azure Media Services, puis cliquez sur bouton Installer de hello.
   
    Hello projet est modifié et fait référence à toohello Extensions Media Services .NET SDK, Media Services .NET SDK, et les autres assemblys dépendants sont ajoutés.
6. toopromote un environnement de développement plus propre, pensez à activer la restauration des packages NuGet. Pour plus d'informations, consultez le document [Restauration du package NuGet](http://docs.nuget.org/consume/package-restore).
7. Ajoutez une référence trop**System.Configuration** assembly. Cet assembly contient hello System.Configuration. **ConfigurationManager** classe qui est utilisé tooaccess des fichiers de configuration (par exemple, App.config).
   
    références tooadd à l’aide de la boîte de dialogue Gérer les références hello, cliquez sur le nom de projet de hello Bonjour l’Explorateur de solutions. Sélectionnez ensuite Ajouter et Références.
   
    boîte de dialogue Gérer les références Hello s’affiche.
8. Sous les assemblys .NET framework, rechercher et sélectionnez l’assembly System.Configuration hello et appuyez sur OK.
9. Ouvrez le fichier App.config de hello et ajoutez un *appSettings* toohello section du fichier.     
   
    Définir les valeurs hello qui sont nécessaires tooconnect toohello API Media Services. Pour plus d’informations, consultez [hello accès API Azure Media Services avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md). 

    Si vous utilisez [l’authentification utilisateur](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) votre fichier de configuration sera probablement ont des valeurs pour votre domaine de locataire Azure AD et hello du point de terminaison AMS REST API.
    
    >[!Important]
    >La plupart des exemples de code Bonjour documentation Azure Media Services définie, utilisez un type (interactif) d’utilisateur de l’authentification tooconnect toohello AMS API. Cette méthode d’authentification fonctionne bien avec les applications natives de gestion ou de surveillance : applications mobiles, applications Windows et applications de console. Cette méthode d’authentification ne convient pas aux applications de type serveur, services web et API.  Pour plus d’informations, consultez [hello accès AMS API avec l’authentification Azure AD](media-services-use-aad-auth-to-access-ams-api.md).

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. Remplacer hello existants **à l’aide de** instructions au début de hello du fichier Program.cs de hello avec hello suivant de code.
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

À ce stade, vous êtes prêt toostart développe une application de Media Services.    

## <a name="example"></a>Exemple

Voici un exemple de petit qui se connecte toohello AMS API et répertorie tous les processeurs multimédias disponibles.
    
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

##<a name="next-steps"></a>Étapes suivantes

Maintenant [vous pouvez vous connecter toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) et démarrer [développement](media-services-dotnet-get-started.md).


## <a name="media-services-learning-paths"></a>Parcours d’apprentissage de Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Fournir des commentaires
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

