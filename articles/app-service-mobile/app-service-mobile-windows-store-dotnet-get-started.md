---
title: aaaCreate une plate-forme de Windows universelle (UWP) qui utilise des applications mobiles | Documents Microsoft
description: "Suivez ce didacticiel tooget un bon départ avec les serveurs principaux de l’application mobile Azure pour le développement d’applications de plateforme Windows universelle (UWP) en c#, Visual Basic ou JavaScript."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a>Créer une application Windows
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Vue d'ensemble
Ce didacticiel vous montre comment tooadd un backend de cloud service application de plateforme Windows universelle (UWP) tooa. Pour plus d’informations, consultez [Que sont les applications Mobile Apps ?](app-service-mobile-value-prop.md). Hello Voici les captures d’écran à partir de l’application hello terminée :

![Application de bureau terminée](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
En cours d’exécution sur un ordinateur de bureau.

![Application de téléphone terminée](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
En cours d’exécution sur un téléphone

Vous devez suivre ce didacticiel avant de pouvoir suivre les autres didacticiels Mobile App pour les applications UWP.

## <a name="prerequisites"></a>Composants requis
toocomplete ce didacticiel, vous devez hello suivant :

* Un compte Azure actif. Si vous n’avez pas un compte, vous pouvez souscrire à la période d’évaluation d’Azure et obtenir des too10 libre les applications mobiles que vous pouvez continuer à utiliser même après la fin de votre version d’évaluation. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio Community 2015] ou version ultérieure.

## <a name="create-a-new-azure-mobile-app-backend"></a>Créer un serveur principal d'applications mobiles Azure
Suivez ces étapes de toocreate un serveur principal de l’application Mobile.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

Vous avez maintenant configuré un serveur principal d’application mobile Azure qui peut être utilisé par vos applications clientes mobiles. Ensuite, vous allez télécharger un projet de serveur pour une simple « liste de tâches » back-end et publiez-le tooAzure.

## <a name="configure-hello-server-project"></a>Configurer le projet de serveur hello
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a>Téléchargez et exécutez le projet de client hello
Une fois que vous avez configuré votre serveur principal de l’application Mobile, vous pouvez créer une application cliente ou modifier un tooAzure de tooconnect application existante. Dans cette section, vous téléchargez un projet de modèle d’application UWP est le principal de l’application Mobile tooyour tooconnect personnalisé.

1. Dans hello **démarrage rapide** panneau pour le service principal de votre application Mobile, cliquez sur **créer une application** > **télécharger**, puis extraire les fichiers de projet hello compressé ordinateur local de tooyour.

    ![Télécharger le projet de démarrage rapide Windows](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. (Facultatif) Ajouter toohello de projet application hello UWP même solution en tant que projet de serveur hello. Cela facilite la toodebug test à la fois hello principal d’application et hello dans hello même solution Visual Studio, si vous choisissez toodo ainsi. tooadd une solution de toohello de projet application UWP, vous devez être à l’aide de Visual Studio 2015 ou une version ultérieure.
3. Application de plateforme Windows universelle hello en tant que projet de démarrage hello, appuyez sur toodeploy de clé F5 hello et application hello d’exécution.
4. Dans l’application hello, tapez un texte explicite, tel que *didacticiel de hello complète*, Bonjour **Insert a TodoItem** zone de texte, puis cliquez sur **enregistrer**.

    ![Démarrage rapide Windows - Bureau terminé](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    Envoie un billet demande toohello application mobile serveur principal qui est hébergé dans Azure.
5. (Facultatif) Arrêter l’application hello et redémarrer sur un autre appareil ou un émulateur mobile.

    ![Démarrage rapide Windows - Téléphone terminé](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    Notez que les données enregistrées à partir de l’étape précédente de hello sont chargées à partir d’Azure après le démarrage de hello application UWP.

## <a name="next-steps"></a>Étapes suivantes
* [Ajouter une application de tooyour d’authentification](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Découvrez comment tooauthenticate les utilisateurs de votre application avec un fournisseur d’identité.
* [Ajouter une application de tooyour de notifications push](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Découvrez comment les notifications push tooadd prennent en charge tooyour application et configurer votre application Mobile back-end toouse Azure Notification Hubs toosend les notifications de transmission.
* [Activer la synchronisation hors connexion pour votre application](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Découvrez comment tooadd hors connexion prennent en charge votre application à l’aide d’un serveur principal de l’application Mobile. Synchronisation hors connexion permet de toointeract les utilisateurs finaux avec une application mobile&mdash;affichage, l’ajout ou la modification des données&mdash;même quand il n’existe aucune connexion réseau.

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203
