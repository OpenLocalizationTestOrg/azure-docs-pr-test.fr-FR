---
title: aaaDeploy une application .NET dans un conteneur de tooAzure Service Fabric | Documents Microsoft
description: "Vous apprend comment toopackage une application .NET dans Visual Studio dans un conteneur Docker. Cette nouvelle application « conteneur » est ensuite déployée cluster Service Fabric de tooa."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: mikhegn
ms.openlocfilehash: 094b0e71d76b2e56ffb9b23638dd8154b3aff5fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-net-application-in-a-windows-container-tooazure-service-fabric"></a>Déployer une application .NET dans un tooAzure de conteneur Windows Service Fabric

Ce didacticiel vous montre comment toodeploy une application ASP.NET existante dans un conteneur Windows sur Azure.

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer un projet Docker dans Visual Studio
> * Mettre en conteneur une application existante
> * Configurer l’intégration continue avec Visual Studio et VSTS

## <a name="prerequisites"></a>Conditions préalables

1. Installez [Docker CE pour Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description) afin que vous puissiez exécuter des conteneurs sur Windows 10.
2. Familiarisez-vous avec hello [démarrage rapide des conteneurs de Windows 10][link-container-quickstart].
3. Télécharger hello [Fabrikam Fiber CallCenter] [ link-fabrikam-github] exemple d’application.
4. Installez [Azure PowerShell][link-azure-powershell-install]
5. Installer hello [extension des outils de livraison continue pour Visual Studio 2017][link-visualstudio-cd-extension]
6. Créez un [Abonnement Azure][link-azure-subscription] et un [Compte Visual Studio Team Services][link-vsts-account]. 
7. [Créez un cluster sur Azure](service-fabric-tutorial-create-cluster-azure-ps.md)

## <a name="containerize-hello-application"></a>Mettez en conteneur application hello

Maintenant que vous avez un [cluster Service Fabric s’exécute dans Azure](service-fabric-tutorial-create-cluster-azure-ps.md) vous êtes prêt toocreate et que vous déployez une application en conteneur. toostart notre application en cours d’exécution dans un conteneur, nous devons tooadd **prise en charge Docker** projet toohello dans Visual Studio. Lorsque vous ajoutez **prise en charge Docker** toohello application, deux événements se produisent. Tout d’abord, un _Dockerfile_ est ajouté toohello projet. Ce nouveau fichier décrit comment image de conteneur hello toobe généré. Puis la deuxième, un nouveau _docker-composer_ projet est ajouté à la solution de toohello. nouveau projet Hello contient quelques docker-composer des fichiers. Fichiers de composer de docker peuvent être utilisé toodescribe comment conteneur de hello est exécuté.

En savoir plus sur l’utilisation de [Visual Studio Container Tools][link-visualstudio-container-tools].

>[!NOTE]
>S’il est hello première fois que vous les images de conteneur Windows sont en cours d’exécution sur votre ordinateur, CE de Docker doit le chercher les images de base hello pour vos conteneurs. les images de Hello utilisés dans ce didacticiel sont 14 Go. Pour commencer, exécutez hello suivant des images de base hello toopull commande Terminal Server :
>```cmd
>docker pull microsoft/mssql-server-windows-developer
>docker pull microsoft/aspnet:4.6.2
>```

### <a name="add-docker-support"></a>Ajouter la prise en charge Docker

Ouvrez hello [FabrikamFiber.CallCenter.sln] [ link-fabrikam-github] fichier dans Visual Studio.

Avec le bouton hello **FabrikamFiber.Web** projet > **ajouter** > **prise en charge Docker**.

### <a name="add-support-for-sql"></a>Ajouter la prise en charge de SQL

Cette application utilise SQL en tant que fournisseur de données hello, par conséquent, un serveur SQL server est requis toorun hello application. Référencez une image de conteneur SQL Server dans notre fichier docker-compose.override.yml.

Dans Visual Studio, ouvrez **l’Explorateur de solutions**, trouver **composer de docker**et ouvrez hello **docker-compose.override.yml**.

Accédez toohello `services:` nœud, ajoutez un nœud nommé `db:` qui définit l’entrée de SQL Server hello pour le conteneur de hello.

```yml
  db:
    image: microsoft/mssql-server-windows-developer
    environment:
      sa_password: "Password1"
      ACCEPT_EULA: "Y"
    ports:
      - "1433"
    healthcheck:
      test: [ "CMD", "sqlcmd", "-U", "sa", "-P", "Password1", "-Q", "select 1" ]
      interval: 1s
      retries: 20
```

>[!NOTE]
>Vous pouvez utiliser l’instance SQL Server de votre choix pour le débogage local, tant qu’elle est accessible à partir de votre hôte. **localdb** ne prend cependant pas en charge la communication `container -> host`.

>[!WARNING]
>L’exécution de SQL Server dans un conteneur ne prend pas en charge les données persistantes. Lorsque le conteneur de hello s’arrête, vos données sont effacées. N’utilisez pas cette configuration pour la production.

Accédez toohello `fabrikamfiber.web:` nœud et ajouter un nœud enfant nommé `depends_on:`. Cela garantit que hello `db` service (conteneur de SQL Server hello) démarre avant que notre application web (fabrikamfiber.web).

```yml
  fabrikamfiber.web:
    depends_on:
      - db
```

### <a name="update-hello-web-config"></a>Mettre à jour hello web config

Dans hello **FabrikamFiber.Web** projet, la chaîne de connexion de mise à jour hello Bonjour **web.config** toopoint toohello SQL Server dans le conteneur de hello, de fichiers.

```xml
<add name="FabrikamFiber-Express" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />

<add name="FabrikamFiber-DataWarehouse" connectionString="Data Source=db,1433;Database=FabrikamFiber;User Id=sa;Password=Password1;MultipleActiveResultSets=True" providerName="System.Data.SqlClient" />
```

>[!NOTE]
>Si vous voulez toouse un autre serveur SQL Server lors de la création d’une version de build de votre application web, ajoutez un autre fichier de web.release.config tooyour chaîne connexion.

### <a name="test-your-container"></a>Tester votre conteneur

Appuyez sur **F5** toorun et déboguer l’application hello dans votre conteneur.

Bord ouvre la page de lancement défini de votre application à l’aide d’adresse IP de hello du conteneur de hello sur le réseau interne NAT (généralement 172.x.x.x) de hello. toolearn en savoir plus sur le débogage d’applications dans des conteneurs à l’aide de Visual Studio 2017, consultez [cet article][link-debug-container].

![exemple de fabrikam dans un conteneur][image-web-preview]

Hello conteneur est maintenant prêt toobe généré et empaqueté dans une application de Service Fabric. Une fois que vous avez hello conteneur génération de l’image sur votre ordinateur, vous pouvez distribuer le Registre de conteneur tooany et par l’extraction vers le bas tooany hôte toorun.

## <a name="get-hello-application-ready-for-hello-cloud"></a>Préparer l’application hello pour le cloud de hello

l’application de hello tooget prête pour l’exécution dans l’infrastructure de Service dans Azure, nous devons toocomplete deux étapes :

1. Exposer le port hello que nous voulons tooreach en mesure de toobe notre application web dans le cluster Service Fabric de hello.
2. Fournir une base de données SQL prête pour notre application.

### <a name="expose-hello-port-for-hello-app"></a>Exposer le port hello pour une application hello
cluster Service Fabric de Hello que nous avons configuré, a port *80* ouvert par défaut dans hello équilibrage de charge Azure, qui équilibre cluster de toohello le trafic entrant. Nous pouvons exposer notre conteneur sur ce port par le biais de notre fichier docker-compose.yml.

Dans Visual Studio, ouvrez **l’Explorateur de solutions**, trouver **composer de docker**et ouvrez hello **docker-compose.override.yml**.

Modifier hello `fabrikamfiber.web:` nœud, ajoutez un nœud enfant nommé `ports:`.

Ajoutez une entrée chaîne `- "80:80"`.

```yml
  version: '3'

  services:
    fabrikamfiber.web:
      image: fabrikamfiber.web
      build:
        context: .\FabrikamFiber.Web
        dockerfile: Dockerfile
      ports:
        - "80:80"
```

### <a name="use-a-production-sql-database"></a>Utiliser une base de données SQL de production
Lors de l’exécution dans un environnement de production, nos données doivent être persistantes dans la base de données. Il n’existe actuellement aucune donnée persistante de façon tooguarantee dans un conteneur, par conséquent vous ne pouvez pas stocker les données de production dans SQL Server dans un conteneur.

Nous vous recommandons d’utiliser une base de données Azure SQL Database. tooset haut et exécuter un serveur SQL géré dans Azure, visitez hello [Démarrages rapides de base de données Azure SQL] [ link-azure-sql] l’article.

>[!NOTE]
>N’oubliez pas de serveur SQL toochange hello connexion chaînes toohello Bonjour **web.release.config** fichier Bonjour **FabrikamFiber.Web** projet.
>
>Cette application échoue normalement si aucune base de données SQL n’est accessible. Vous pouvez choisir toogo avance et déployer l’application hello avec aucun serveur SQL server.

## <a name="deploy-with-visual-studio-team-services"></a>Déployer avec Visual Studio Team Services

tooset le déploiement à l’aide de Visual Studio Team Services, vous devez tooinstall hello [extension des outils de livraison continue pour Visual Studio 2017][link-visualstudio-cd-extension]. Cette extension rend facile toodeploy tooAzure par la configuration de Visual Studio Team Services et obtenir votre cluster Service Fabric de tooyour application déployée.

tooget démarré, votre code doit être hébergé dans le contrôle de code source. reste Hello de cette section suppose que **git** est utilisé.

### <a name="set-up-a-vsts-repo"></a>Configurer un référentiel VSTS
En hello en bas à droite de Visual Studio, cliquez sur **ajouter tooSource contrôle** > **Git** (ou de l’option que vous préférez).

![Appuyez sur le bouton de contrôle de source de hello][image-source-control]

Bonjour _Team Explorer_ volet, appuyez sur **publier le référentiel Git**.

Sélectionnez le nom de votre dépôt VSTS et appuyez sur **Dépôt**.

![publier le référentiel tooVSTS][image-publish-repo]

Maintenant que votre code est synchronisé avec un dépôt de code source VSTS, vous pouvez configurer l’intégration continue et la livraison continue.

### <a name="setup-continuous-delivery"></a>Configurer une livraison continue

Dans _l’Explorateur de solutions_, avec le bouton hello **solution** > **configurer la livraison continue**.

Sélectionnez hello abonnement Azure.

Définissez **Type d’hôte** trop**Cluster Service Fabric**.

Définissez **hôte cible** toohello cluster service fabric vous avez créé dans la section précédente de hello.

Choisissez un **Registre de conteneur** toopublish à votre conteneur.

>[!TIP]
>Hello d’utilisation **modifier** bouton toocreate un Registre de conteneur.

Appuyez sur **OK**.

![configurer l’intégration continue pour service fabric][image-setup-ci]
   
   Une fois la configuration hello est terminée, votre conteneur est déployé tooService l’ensemble fibre optique. Chaque fois que vous effectuez un push référentiel toohello de mises à jour une nouvelle build et la version est exécutée.
   
   >[!NOTE]
   >Images de conteneur de construction hello prennent environ 15 minutes.
   >Hello premier déploiement toohello Service Fabric cluster entraîne hello base Windows Server Core conteneur images toobe téléchargé. téléchargement de Hello prend plus de 5 à 10 minutes toocomplete.

Parcourir l’application de centre d’appels Fabrikam toohello à l’aide des url hello de votre cluster : par exemple, *http://mycluster.westeurope.cloudapp.azure.com*

Maintenant que vous avez placées dans des conteneurs et déployé la solution de centre d’appels Fabrikam hello, vous pouvez ouvrir hello [portail Azure] [ link-azure-portal] et voir l’application hello en cours d’exécution dans l’infrastructure de Service. application de hello tootry, ouvrez un navigateur web et accédez toohello des URL de votre cluster Service Fabric.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Créer un projet Docker dans Visual Studio
> * Mettre en conteneur une application existante
> * Configurer l’intégration continue avec Visual Studio et VSTS

<!--   NOTE SURE WHAT WE SHOULD DO YET HERE

Advance toohello next tutorial toolearn how toobind a custom SSL certificate tooit.

> [!div class="nextstepaction"]
> [Bind an existing custom SSL certificate tooAzure Web Apps](app-service-web-tutorial-custom-ssl.md)

## Next steps

- [Container Tooling in Visual Studio][link-visualstudio-container-tools]
- [Get started with containers in Service Fabric][link-servicefabric-containers]
- [Creating Service Fabric applications][link-servicefabric-createapp]
-->

[link-debug-container]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-fabrikam-github]: https://aka.ms/fabrikamcontainer
[link-container-quickstart]: /virtualization/windowscontainers/quick-start/quick-start-windows-10
[link-visualstudio-container-tools]: /dotnet/articles/core/docker/visual-studio-tools-for-docker
[link-azure-powershell-install]: /powershell/azure/install-azurerm-ps
[link-servicefabric-create-secure-clusters]: service-fabric-cluster-creation-via-arm.md
[link-visualstudio-cd-extension]: https://aka.ms/cd4vs
[link-servicefabric-containers]: service-fabric-get-started-containers.md
[link-servicefabric-createapp]: service-fabric-create-your-first-application-in-visual-studio.md
[link-azure-portal]: https://portal.azure.com
[link-sf-clustertemplate]: https://aka.ms/securepreviewonelineclustertemplate
[link-azure-pricing-calculator]: https://azure.microsoft.com/en-us/pricing/calculator/
[link-azure-subscription]: https://azure.microsoft.com/en-us/free/
[link-vsts-account]: https://www.visualstudio.com/team-services/pricing/
[link-azure-sql]: /azure/sql-database/

[image-web-preview]: media/service-fabric-host-app-in-a-container/fabrikam-web-sample.png
[image-source-control]: media/service-fabric-host-app-in-a-container/add-to-source-control.png
[image-publish-repo]: media/service-fabric-host-app-in-a-container/publish-repo.png
[image-setup-ci]: media/service-fabric-host-app-in-a-container/configure-continuous-integration.png
