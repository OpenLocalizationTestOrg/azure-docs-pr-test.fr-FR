---
title: "aaaDevelop localement avec hello Azure Cosmos DB émulateur | Documents Microsoft"
description: "À l’aide de hello Azure Cosmos DB émulateur, vous pouvez développer et tester votre application localement pour gratuitement, sans créer un abonnement Azure."
services: cosmos-db
documentationcenter: 
keywords: "Émulateur Azure Cosmos DB"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="ba733-104">Utilisez hello Azure Cosmos DB émulateur pour développement local et le test</span><span class="sxs-lookup"><span data-stu-id="ba733-104">Use hello Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="ba733-105"><strong>Fichiers binaires</strong></span><span class="sxs-lookup"><span data-stu-id="ba733-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="ba733-106">Télécharger MSI</span><span class="sxs-lookup"><span data-stu-id="ba733-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="ba733-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="ba733-108">Docker Hub</span><span class="sxs-lookup"><span data-stu-id="ba733-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-109"><strong>Source Docker</strong></span><span class="sxs-lookup"><span data-stu-id="ba733-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="ba733-110">Github</span><span class="sxs-lookup"><span data-stu-id="ba733-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="ba733-111">Bonjour Azure Cosmos DB émulateur fournit un environnement local qui émule hello service de base de données Azure Cosmos à des fins de développement.</span><span class="sxs-lookup"><span data-stu-id="ba733-111">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="ba733-112">Hello Azure Cosmos DB émulateur vous pouvez de développer et tester votre application localement, sans créer un abonnement Azure ou de subir les coûts.</span><span class="sxs-lookup"><span data-stu-id="ba733-112">Using hello Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="ba733-113">Lorsque vous êtes satisfait de la façon dont votre application fonctionne Bonjour Azure Cosmos DB émulateur, vous pouvez basculer toousing un compte de base de données Azure Cosmos dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-113">When you're satisfied with how your application is working in hello Azure Cosmos DB Emulator, you can switch toousing an Azure Cosmos DB account in hello cloud.</span></span>

<span data-ttu-id="ba733-114">Cet article traite des hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="ba733-114">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="ba733-115">Lors de l’installation hello émulateur</span><span class="sxs-lookup"><span data-stu-id="ba733-115">Installing hello Emulator</span></span>
> * <span data-ttu-id="ba733-116">Hello émulateur en cours d’exécution sur Docker pour Windows</span><span class="sxs-lookup"><span data-stu-id="ba733-116">Running hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="ba733-117">Authentification des demandes</span><span class="sxs-lookup"><span data-stu-id="ba733-117">Authenticating requests</span></span>
> * <span data-ttu-id="ba733-118">À l’aide de hello Explorateur de données dans l’émulateur de hello</span><span class="sxs-lookup"><span data-stu-id="ba733-118">Using hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="ba733-119">Exportation de certificats SSL</span><span class="sxs-lookup"><span data-stu-id="ba733-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="ba733-120">Appel de hello émulateur à partir de la ligne de commande hello</span><span class="sxs-lookup"><span data-stu-id="ba733-120">Calling hello Emulator from hello command line</span></span>
> * <span data-ttu-id="ba733-121">Collecte des fichiers de trace</span><span class="sxs-lookup"><span data-stu-id="ba733-121">Collecting trace files</span></span>

<span data-ttu-id="ba733-122">Nous vous recommandons de mise en route en regardant hello suivant vidéo, où Kirill Gavrylyuk montre comment tooget démarrer avec hello Azure Cosmos DB émulateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-122">We recommend getting started by watching hello following video, where Kirill Gavrylyuk shows how tooget started with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="ba733-123">Notez que la vidéo de hello sous l’appellation toohello émulateur hello DocumentDB émulateur, mais outil hello lui-même a été renommé Bonjour Azure Cosmos DB émulateur depuis touchant vidéo de hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-123">Note that hello video refers toohello emulator as hello DocumentDB Emulator, but hello tool itself has been renamed hello Azure Cosmos DB Emulator since taping hello video.</span></span> <span data-ttu-id="ba733-124">Toutes les informations Bonjour vidéo sont toujours exactes pour hello Azure Cosmos DB émulateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-124">All information in hello video is still accurate for hello Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a><span data-ttu-id="ba733-125">Fonctionne de hello émulateur</span><span class="sxs-lookup"><span data-stu-id="ba733-125">How hello Emulator works</span></span>
<span data-ttu-id="ba733-126">Bonjour Azure Cosmos DB émulateur fournit une émulation haute fidélité de hello service de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ba733-126">hello Azure Cosmos DB Emulator provides a high-fidelity emulation of hello Azure Cosmos DB service.</span></span> <span data-ttu-id="ba733-127">Il prend en charge les mêmes fonctionnalités qu’Azure Cosmos DB, notamment la prise en charge de la création et de l’interrogation des documents JSON, la configuration et la mise à l’échelle des collections, et l’exécution des procédures stockées et des déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="ba733-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="ba733-128">Vous pouvez développer et tester des applications à l’aide de hello Azure Cosmos DB émulateur et les déployer tooAzure à une échelle globale faisant simplement une seule configuration modifier le point de terminaison de connexion toohello pour la base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ba733-128">You can develop and test applications using hello Azure Cosmos DB Emulator, and deploy them tooAzure at global scale by just making a single configuration change toohello connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="ba733-129">Pendant que nous avons créé une émulation locale haute fidélité du service de base de données Azure Cosmos réel hello, implémentation hello Hello Azure Cosmos DB émulateur est différente de celui du service de hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-129">While we created a high-fidelity local emulation of hello actual Azure Cosmos DB service, hello implementation of hello Azure Cosmos DB Emulator is different than that of hello service.</span></span> <span data-ttu-id="ba733-130">Par exemple, hello Azure Cosmos DB émulateur utilise les composants du système d’exploitation standard tels que système de fichiers local hello pour la persistance et la pile de protocole HTTPS pour la connectivité.</span><span class="sxs-lookup"><span data-stu-id="ba733-130">For example, hello Azure Cosmos DB Emulator uses standard OS components such as hello local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="ba733-131">Cela signifie que certaines fonctionnalités qui s’appuie sur l’infrastructure Azure telles que réplication globale, une latence chiffre millisecondes pour les lectures/écritures et les niveaux de cohérence paramétrables ne sont pas disponibles via hello Azure Cosmos DB émulateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via hello Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="ba733-132">À ce hello temps Explorateur de données Bonjour émulateur prend uniquement en charge la création des collections de l’API DocumentDB et MongoDB hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-132">At this time hello Data Explorer in hello emulator only supports hello creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="ba733-133">Hello Explorateur de données dans l’émulateur de hello ne prend pas en charge la création de tables et graphiques hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-133">hello Data Explorer in hello emulator does not currently support hello creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="ba733-134">Conditions requises pour le système</span><span class="sxs-lookup"><span data-stu-id="ba733-134">System requirements</span></span>
<span data-ttu-id="ba733-135">Bonjour Azure Cosmos DB émulateur a hello suivant les exigences matérielles et logicielles :</span><span class="sxs-lookup"><span data-stu-id="ba733-135">hello Azure Cosmos DB Emulator has hello following hardware and software requirements:</span></span>

* <span data-ttu-id="ba733-136">Configuration logicielle requise</span><span class="sxs-lookup"><span data-stu-id="ba733-136">Software requirements</span></span>
  * <span data-ttu-id="ba733-137">Windows Server 2012 R2, Windows Server 2016 ou Windows 10</span><span class="sxs-lookup"><span data-stu-id="ba733-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="ba733-138">Conditions matérielles minimales requises</span><span class="sxs-lookup"><span data-stu-id="ba733-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="ba733-139">2 Go de RAM</span><span class="sxs-lookup"><span data-stu-id="ba733-139">2 GB RAM</span></span>
  * <span data-ttu-id="ba733-140">10 Go d’espace disque disponible</span><span class="sxs-lookup"><span data-stu-id="ba733-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="ba733-141">Installation</span><span class="sxs-lookup"><span data-stu-id="ba733-141">Installation</span></span>
<span data-ttu-id="ba733-142">Vous pouvez télécharger et installer hello Azure Cosmos DB émulateur à partir de hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="ba733-142">You can download and install hello Azure Cosmos DB Emulator from hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="ba733-143">tooinstall, configurer et exécuter hello Azure Cosmos DB émulateur, vous devez disposer des privilèges d’administrateur sur l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-143">tooinstall, configure, and run hello Azure Cosmos DB Emulator, you must have administrative privileges on hello computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="ba733-144">Exécution de Docker pour Windows</span><span class="sxs-lookup"><span data-stu-id="ba733-144">Running on Docker for Windows</span></span>

<span data-ttu-id="ba733-145">Bonjour Azure Cosmos DB émulateur peut être exécuté sur Docker pour Windows.</span><span class="sxs-lookup"><span data-stu-id="ba733-145">hello Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="ba733-146">Hello émulateur ne fonctionne pas sur Docker pour Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="ba733-146">hello Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="ba733-147">Une fois que vous avez [Docker pour Windows](https://www.docker.com/docker-windows) installé, vous pouvez extraire image de l’émulateur hello à partir du Hub d’ancrage en exécutant hello de commande suivante à partir de votre favori interpréteur de commandes (cmd.exe, PowerShell, etc..).</span><span class="sxs-lookup"><span data-stu-id="ba733-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull hello Emulator image from Docker Hub by running hello following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="ba733-148">image de hello toostart, exécutez hello suivant les commandes.</span><span class="sxs-lookup"><span data-stu-id="ba733-148">toostart hello image, run hello following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="ba733-149">réponse de Hello semble similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="ba733-149">hello response looks similar toohello following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="ba733-150">Fermeture hello shell interactif une fois hello émulateur a été démarré sera le conteneur de l’émulateur arrêt hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-150">Closing hello interactive shell once hello Emulator has been started will shutdown hello Emulator’s container.</span></span>

<span data-ttu-id="ba733-151">Utiliser le point de terminaison hello et la clé principale dans à partir de la réponse de hello dans votre client et importer le certificat SSL de hello dans votre hôte.</span><span class="sxs-lookup"><span data-stu-id="ba733-151">Use hello endpoint and master key in from hello response in your client and import hello SSL certificate into your host.</span></span> <span data-ttu-id="ba733-152">tooimport hello certificat SSL, procédez comme hello suivant à partir d’une invite de commandes administrateur :</span><span class="sxs-lookup"><span data-stu-id="ba733-152">tooimport hello SSL certificate, do hello following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a><span data-ttu-id="ba733-153">Démarrer l’émulateur de hello</span><span class="sxs-lookup"><span data-stu-id="ba733-153">Start hello Emulator</span></span>

<span data-ttu-id="ba733-154">toostart hello Azure Cosmos DB émulateur, sélectionnez le bouton Démarrer de hello ou appuyez sur Windows hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-154">toostart hello Azure Cosmos DB Emulator, select hello Start button or press hello Windows key.</span></span> <span data-ttu-id="ba733-155">Commencez à taper **Azure Cosmos DB émulateur**et l’émulateur hello select à partir de la liste des applications hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-155">Begin typing **Azure Cosmos DB Emulator**, and select hello emulator from hello list of applications.</span></span> 

![Sélectionnez hello bouton ou appuyez sur hello Windows touche, commencez à taper ** Azure Cosmos DB émulateur ** et émulateur hello select à partir de la liste des applications hello](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="ba733-157">Lors de l’émulateur de hello est en cours d’exécution, vous verrez une icône Bonjour zone de notification de la barre des tâches Windows.</span><span class="sxs-lookup"><span data-stu-id="ba733-157">When hello emulator is running, you'll see an icon in hello Windows taskbar notification area.</span></span> ![Notification dans la barre des tâches de l'émulateur local Azure Cosmos DB](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="ba733-159">Bonjour Azure Cosmos DB émulateur par défaut s’exécute sur l’ordinateur local hello (« localhost ») à l’écoute sur le port 8081.</span><span class="sxs-lookup"><span data-stu-id="ba733-159">hello Azure Cosmos DB Emulator by default runs on hello local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="ba733-160">Émulateur de base de données Azure Cosmos Hello est installé par défaut toohello `C:\Program Files\Azure Cosmos DB Emulator` active.</span><span class="sxs-lookup"><span data-stu-id="ba733-160">hello Azure Cosmos DB Emulator is installed by default toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="ba733-161">Vous pouvez également démarrer et arrêter l’émulateur hello hello de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="ba733-161">You can also start and stop hello emulator from hello command-line.</span></span> <span data-ttu-id="ba733-162">Pour plus d’informations, consultez la section [Référence de l’outil en ligne de commande](#command-line).</span><span class="sxs-lookup"><span data-stu-id="ba733-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="ba733-163">Démarrer l’Explorateur de données</span><span class="sxs-lookup"><span data-stu-id="ba733-163">Start Data Explorer</span></span>

<span data-ttu-id="ba733-164">Lancement de l’émulateur de base de données Azure Cosmos hello s’ouvre automatiquement hello Explorateur de données de base de données Azure Cosmos dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-164">When hello Azure Cosmos DB emulator launches it will automatically open hello Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="ba733-165">adresse de Hello apparaîtront en tant que [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="ba733-165">hello address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="ba733-166">Si vous fermez hello explorer et aimeriez toore-open il ultérieurement, vous pouvez ouvrir les URL de hello dans votre navigateur ou lancer à partir de hello Azure Cosmos DB émulateur Bonjour icône Windows comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ba733-166">If you close hello explorer and would like toore-open it later, you can either open hello URL in your browser or launch it from hello Azure Cosmos DB Emulator in hello Windows Tray Icon as shown below.</span></span>

![Lanceur de l’Explorateur de données de l’émulateur local Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="ba733-168">Recherche de mises à jour</span><span class="sxs-lookup"><span data-stu-id="ba733-168">Checking for updates</span></span>
<span data-ttu-id="ba733-169">L’Explorateur de données indique si une nouvelle mise à jour est disponible en téléchargement.</span><span class="sxs-lookup"><span data-stu-id="ba733-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="ba733-170">Les données créées dans une version de hello Azure Cosmos DB émulateur ne sont pas garanties toobe accessible lorsque vous utilisez une version différente.</span><span class="sxs-lookup"><span data-stu-id="ba733-170">Data created in one version of hello Azure Cosmos DB Emulator is not guaranteed toobe accessible when using a different version.</span></span> <span data-ttu-id="ba733-171">Si vous avez besoin à toopersist vos données à long terme la hello, il est recommandé que vous stockez ces données dans un compte de base de données Azure Cosmos, plutôt que dans hello Azure Cosmos DB émulateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-171">If you need toopersist your data for hello long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in hello Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="ba733-172">Authentification des demandes</span><span class="sxs-lookup"><span data-stu-id="ba733-172">Authenticating requests</span></span>
<span data-ttu-id="ba733-173">Tout comme avec la base de données Azure Cosmos dans le cloud de hello, chaque demande que vous apportez sur hello Azure Cosmos DB émulateur doit être authentifiée.</span><span class="sxs-lookup"><span data-stu-id="ba733-173">Just as with Azure Cosmos DB in hello cloud, every request that you make against hello Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="ba733-174">Bonjour Azure Cosmos DB émulateur prend en charge un seul compte fixe et une clé d’authentification connu pour l’authentification de clé principale.</span><span class="sxs-lookup"><span data-stu-id="ba733-174">hello Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="ba733-175">Ce compte et la clé sont hello seules informations d’identification autorisées pour une utilisation avec hello Azure Cosmos DB émulateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-175">This account and key are hello only credentials permitted for use with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="ba733-176">Il s'agit de :</span><span class="sxs-lookup"><span data-stu-id="ba733-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="ba733-177">clé principale de Hello pris en charge par hello Azure Cosmos DB émulateur est destinée à être utilisé uniquement avec l’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-177">hello master key supported by hello Azure Cosmos DB Emulator is intended for use only with hello emulator.</span></span> <span data-ttu-id="ba733-178">Vous ne pouvez pas utiliser votre compte de base de données Azure Cosmos de production et votre clé avec hello Azure Cosmos DB émulateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-178">You cannot use your production Azure Cosmos DB account and key with hello Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="ba733-179">Si vous avez démarré l’émulateur de hello avec hello option / Key, puis utiliser une clé hello généré au lieu de « C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw == »</span><span class="sxs-lookup"><span data-stu-id="ba733-179">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="ba733-180">En outre, tout comme hello service de base de données Azure Cosmos, hello Azure Cosmos DB émulateur prend en charge uniquement une communication sécurisée via SSL.</span><span class="sxs-lookup"><span data-stu-id="ba733-180">Additionally, just as hello Azure Cosmos DB service, hello Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-hello-emulator-on-a-local-network"></a><span data-ttu-id="ba733-181">Émulateur de hello en cours d’exécution sur un réseau local</span><span class="sxs-lookup"><span data-stu-id="ba733-181">Running hello emulator on a local network</span></span>

<span data-ttu-id="ba733-182">Vous pouvez exécuter l’émulateur de hello sur un réseau local.</span><span class="sxs-lookup"><span data-stu-id="ba733-182">You can run hello emulator on a local network.</span></span> <span data-ttu-id="ba733-183">tooenable accès réseau, spécifiez l’option /AllowNetworkAccess hello au hello [ligne de commande](#command-line-syntax), ce qui nécessite également que vous spécifiez/KEY = key_string ou/keyfile = nom_fichier.</span><span class="sxs-lookup"><span data-stu-id="ba733-183">tooenable network access, specify hello /AllowNetworkAccess option at hello [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="ba733-184">Vous pouvez utiliser /GenKeyFile = nom_fichier toogenerate un fichier avec une clé aléatoire dès le départ.</span><span class="sxs-lookup"><span data-stu-id="ba733-184">You can use /GenKeyFile=file_name toogenerate a file with a random key upfront.</span></span>  <span data-ttu-id="ba733-185">Vous pouvez passer ce trop/KeyFile = nom_fichier ou/Key = contents_of_file.</span><span class="sxs-lookup"><span data-stu-id="ba733-185">Then you can pass that too/KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="ba733-186">un accès réseau pour l’utilisateur hello hello tooenable doit arrêter l’émulateur hello et supprimer le répertoire de données de l’émulateur hello (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="ba733-186">tooenable network access for hello first time hello user should shutdown hello emulator and delete hello emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-hello-emulator"></a><span data-ttu-id="ba733-187">Développement avec hello émulateur</span><span class="sxs-lookup"><span data-stu-id="ba733-187">Developing with hello Emulator</span></span>
<span data-ttu-id="ba733-188">Une fois que vous avez hello Azure Cosmos DB émulateur en cours d’exécution sur votre bureau, vous pouvez utiliser une prise en charge [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) ou hello [API REST de Azure Cosmos DB](/rest/api/documentdb/) toointeract avec hello émulateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-188">Once you have hello Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract with hello Emulator.</span></span> <span data-ttu-id="ba733-189">Bonjour Azure Cosmos DB émulateur inclut également un Explorateur de données intégrés qui vous permet de créer des regroupements pour hello DocumentDB MongoDB APIs et d’afficher et modifier des documents sans écrire de code.</span><span class="sxs-lookup"><span data-stu-id="ba733-189">hello Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for hello DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="ba733-190">Si vous utilisez [prise en charge de base de données Azure Cosmos protocole pour MongoDB](mongodb-introduction.md), utilisez hello suivant de chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="ba733-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use hello following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="ba733-191">Vous pouvez utiliser les outils existants tels que [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB émulateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="ba733-192">Vous pouvez également migrer des données entre hello Azure Cosmos DB émulateur et le service de base de données Azure Cosmos hello à l’aide de hello [outil de Migration de données Azure Cosmos DB](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="ba733-192">You can also migrate data between hello Azure Cosmos DB Emulator and hello Azure Cosmos DB service using hello [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="ba733-193">Si vous avez démarré l’émulateur de hello avec hello option / Key, puis utiliser une clé hello généré au lieu de « C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw == »</span><span class="sxs-lookup"><span data-stu-id="ba733-193">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="ba733-194">À l’aide d’émulateur de base de données Azure Cosmos hello, par défaut, vous pouvez créer des collections de partitions uniques too25 ou 1 collection partitionnée.</span><span class="sxs-lookup"><span data-stu-id="ba733-194">Using hello Azure Cosmos DB emulator, by default, you can create up too25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="ba733-195">Pour plus d’informations sur la modification de cette valeur, consultez [définition hello PartitionCount valeur](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="ba733-195">For more information about changing this value, see [Setting hello PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-hello-ssl-certificate"></a><span data-ttu-id="ba733-196">Exporter le certificat SSL de hello</span><span class="sxs-lookup"><span data-stu-id="ba733-196">Export hello SSL certificate</span></span>

<span data-ttu-id="ba733-197">Langages .NET et toosecurely de magasin de certificats Windows runtime utilisez hello connectent émulateur local de base de données Azure Cosmos toohello.</span><span class="sxs-lookup"><span data-stu-id="ba733-197">.NET languages and runtime use hello Windows Certificate Store toosecurely connect toohello Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="ba733-198">D’autres langages ont leur propre méthode de gestion et de l’utilisation des certificats.</span><span class="sxs-lookup"><span data-stu-id="ba733-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="ba733-199">Java utilise son propre [magasin de certificats](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), tandis que Python utilise des [wrappers de socket](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="ba733-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="ba733-200">Dans l’ordre tooobtain un toouse de certificat avec les langues et runtimes qui ne s’intègrent pas avec hello magasin de certificats Windows vous en aurez besoin tooexport à l’aide de hello Gestionnaire de certificats Windows.</span><span class="sxs-lookup"><span data-stu-id="ba733-200">In order tooobtain a certificate toouse with languages and runtimes that do not integrate with hello Windows Certificate Store you will need tooexport it using hello Windows Certificate Manager.</span></span> <span data-ttu-id="ba733-201">Vous pouvez démarrer, exécutez certlm.msc ou suivez les instructions étape par étape de hello dans [exporter hello Azure Cosmos DB émulateur certificats](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="ba733-201">You can start it by running certlm.msc or follow hello step by step instructions in [Export hello Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="ba733-202">Une fois que le Gestionnaire de certificats hello est en cours d’exécution, hello ouvrir les certificats personnels comme indiqué ci-dessous et l’exportation hello certificat avec le nom convivial hello « DocumentDBEmulatorCertificate » comme fichier X.509 (.cer) d’encodé en BASE-64.</span><span class="sxs-lookup"><span data-stu-id="ba733-202">Once hello certificate manager is running, open hello Personal Certificates as shown below and export hello certificate with hello friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Certificat SSL de l’émulateur local Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="ba733-204">certificat X.509 de Hello peut être importé dans le magasin de certificats hello Java en suivant les instructions de hello dans [Ajout d’un toohello certificat magasin de certificats d’autorité de certification Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="ba733-204">hello X.509 certificate can be imported into hello Java certificate store by following hello instructions in [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="ba733-205">Une fois que le certificat de hello est importé dans le magasin de certificats hello, des applications Java et MongoDB sera en mesure de tooconnect toohello Azure Cosmos DB émulateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-205">Once hello certificate is imported into hello certificate store, Java and MongoDB applications will be able tooconnect toohello Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="ba733-206">Lors de la connexion toohello émulateur à partir de Python et Node.js kits de développement logiciel, la vérification SSL est désactivée.</span><span class="sxs-lookup"><span data-stu-id="ba733-206">When connecting toohello emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="ba733-207"><a id="command-line"></a>Référence sur l’outil en ligne de commande</span><span class="sxs-lookup"><span data-stu-id="ba733-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="ba733-208">À partir de l’emplacement d’installation hello, vous pouvez utiliser toostart de ligne de commande de hello et arrêter l’émulateur de hello, configurer les options et effectuer d’autres opérations.</span><span class="sxs-lookup"><span data-stu-id="ba733-208">From hello installation location, you can use hello command-line toostart and stop hello emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="ba733-209">Syntaxe de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="ba733-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="ba733-210">liste de hello tooview des options de type `CosmosDB.Emulator.exe /?` à l’invite de commandes hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-210">tooview hello list of options, type `CosmosDB.Emulator.exe /?` at hello command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="ba733-211"><strong>Option</strong></span><span class="sxs-lookup"><span data-stu-id="ba733-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="ba733-212"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="ba733-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="ba733-213"><strong>Commande</strong></span><span class="sxs-lookup"><span data-stu-id="ba733-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="ba733-214"><strong>Arguments</strong></span><span class="sxs-lookup"><span data-stu-id="ba733-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-215">[aucun argument]</span><span class="sxs-lookup"><span data-stu-id="ba733-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="ba733-216">Démarre hello Azure Cosmos DB émulateur avec les paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="ba733-216">Starts up hello Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="ba733-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="ba733-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-218">[Aide]</span><span class="sxs-lookup"><span data-stu-id="ba733-218">[Help]</span></span></td>
  <td><span data-ttu-id="ba733-219">Affiche la liste hello de prise en charge des arguments de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="ba733-219">Displays hello list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="ba733-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="ba733-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-221">Shutdown</span><span class="sxs-lookup"><span data-stu-id="ba733-221">Shutdown</span></span></td>
  <td><span data-ttu-id="ba733-222">Bonjour Azure Cosmos DB émulateur s’arrête.</span><span class="sxs-lookup"><span data-stu-id="ba733-222">Shuts down hello Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="ba733-223">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="ba733-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-224">DataPath</span><span class="sxs-lookup"><span data-stu-id="ba733-224">DataPath</span></span></td>
  <td><span data-ttu-id="ba733-225">Spécifie le chemin d’accès hello dans les fichiers de données toostore.</span><span class="sxs-lookup"><span data-stu-id="ba733-225">Specifies hello path in which toostore data files.</span></span> <span data-ttu-id="ba733-226">La valeur par défaut est %LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="ba733-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="ba733-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span><span class="sxs-lookup"><span data-stu-id="ba733-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="ba733-228">&lt;datapath&gt; : un chemin accessible</span><span class="sxs-lookup"><span data-stu-id="ba733-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-229">Port</span><span class="sxs-lookup"><span data-stu-id="ba733-229">Port</span></span></td>
  <td><span data-ttu-id="ba733-230">Spécifie les toouse de numéro de port hello pour l’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-230">Specifies hello port number toouse for hello emulator.</span></span>  <span data-ttu-id="ba733-231">La valeur par défaut est 8081.</span><span class="sxs-lookup"><span data-stu-id="ba733-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="ba733-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span><span class="sxs-lookup"><span data-stu-id="ba733-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="ba733-233">&lt;port&gt; : numéro de port unique</span><span class="sxs-lookup"><span data-stu-id="ba733-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="ba733-234">MongoPort</span></span></td>
  <td><span data-ttu-id="ba733-235">Spécifie les toouse de numéro de port hello pour la compatibilité MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="ba733-235">Specifies hello port number toouse for MongoDB compatibility API.</span></span> <span data-ttu-id="ba733-236">La valeur par défaut est 10255.</span><span class="sxs-lookup"><span data-stu-id="ba733-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="ba733-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="ba733-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="ba733-238">&lt;mongoport&gt; : numéro de port unique</span><span class="sxs-lookup"><span data-stu-id="ba733-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="ba733-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="ba733-240">Spécifie les toouse de ports hello pour une connectivité directe.</span><span class="sxs-lookup"><span data-stu-id="ba733-240">Specifies hello ports toouse for direct connectivity.</span></span> <span data-ttu-id="ba733-241">Les valeurs par défaut sont 10251,10252,10253,10254.</span><span class="sxs-lookup"><span data-stu-id="ba733-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="ba733-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="ba733-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="ba733-243">&lt;directports&gt; : liste séparée par des virgules de 4 ports</span><span class="sxs-lookup"><span data-stu-id="ba733-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-244">Clé</span><span class="sxs-lookup"><span data-stu-id="ba733-244">Key</span></span></td>
  <td><span data-ttu-id="ba733-245">Clé d’autorisation de l’émulateur de hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-245">Authorization key for hello emulator.</span></span> <span data-ttu-id="ba733-246">Clé doit être hello codage en base 64 d’un vecteur de 64 octets.</span><span class="sxs-lookup"><span data-stu-id="ba733-246">Key must be hello base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="ba733-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span><span class="sxs-lookup"><span data-stu-id="ba733-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="ba733-248">&lt;clé&gt;: la clé doit être hello codage en base 64 d’un vecteur de 64 octets</span><span class="sxs-lookup"><span data-stu-id="ba733-248">&lt;key&gt;: Key must be hello base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="ba733-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="ba733-250">Spécifie que le comportement de limitation de taux de demandes est activé.</span><span class="sxs-lookup"><span data-stu-id="ba733-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="ba733-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="ba733-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="ba733-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="ba733-253">Spécifie que le comportement de limitation de taux de demandes est désactivé.</span><span class="sxs-lookup"><span data-stu-id="ba733-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="ba733-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="ba733-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="ba733-255">NoUI</span></span></td>
  <td><span data-ttu-id="ba733-256">Ne pas afficher les émulateur hello interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-256">Do not show hello emulator user interface.</span></span></td>
  <td><span data-ttu-id="ba733-257">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="ba733-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="ba733-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="ba733-259">Ne pas afficher l’Explorateur de documents au démarrage.</span><span class="sxs-lookup"><span data-stu-id="ba733-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="ba733-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="ba733-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="ba733-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="ba733-262">Spécifie le nombre maximal de hello de collections partitionnées.</span><span class="sxs-lookup"><span data-stu-id="ba733-262">Specifies hello maximum number of partitioned collections.</span></span> <span data-ttu-id="ba733-263">Consultez [modifier nombre hello de collections](#set-partitioncount) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="ba733-263">See [Change hello number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="ba733-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="ba733-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="ba733-265">&lt;partitioncount&gt; : nombre maximal autorisé de collections à partition unique.</span><span class="sxs-lookup"><span data-stu-id="ba733-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="ba733-266">Valeur par défaut : 25.</span><span class="sxs-lookup"><span data-stu-id="ba733-266">Default is 25.</span></span> <span data-ttu-id="ba733-267">Valeur maximale autorisée : 250.</span><span class="sxs-lookup"><span data-stu-id="ba733-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="ba733-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="ba733-269">Spécifie le nombre de partitions pour une collection partitionnée par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-269">Specifies hello default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="ba733-270">CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="ba733-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="ba733-271">&lt;defaultpartitioncount&gt; La valeur par défaut est 25.</span><span class="sxs-lookup"><span data-stu-id="ba733-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="ba733-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="ba733-273">Permet l’accès toohello émulateur sur un réseau.</span><span class="sxs-lookup"><span data-stu-id="ba733-273">Enables access toohello emulator over a network.</span></span> <span data-ttu-id="ba733-274">Vous devez également passer/Key =&lt;key_string&gt; ou/keyfile =&lt;nom_fichier&gt; tooenable un accès au réseau.</span><span class="sxs-lookup"><span data-stu-id="ba733-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; tooenable network access.</span></span></td>
  <td><span data-ttu-id="ba733-275">CosmosDB.Emulator.exe AllowNetworkAccess /Key =&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="ba733-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="ba733-276">ou</span><span class="sxs-lookup"><span data-stu-id="ba733-276">or</span></span><br><br><span data-ttu-id="ba733-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span><span class="sxs-lookup"><span data-stu-id="ba733-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="ba733-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="ba733-279">Ne pas ajuster les règles de pare-feu lors de l’utilisation de /AllowNetworkAccess.</span><span class="sxs-lookup"><span data-stu-id="ba733-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="ba733-280">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="ba733-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="ba733-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="ba733-282">Générer une clé d’autorisation de fichier et enregistrez-le toohello spécifié.</span><span class="sxs-lookup"><span data-stu-id="ba733-282">Generate a new authorization key and save toohello specified file.</span></span> <span data-ttu-id="ba733-283">clé de Hello généré peut être utilisée avec hello/KEY ou les options/keyfile.</span><span class="sxs-lookup"><span data-stu-id="ba733-283">hello generated key can be used with hello /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="ba733-284">CosmosDB.Emulator.exe /GenKeyFile =&lt;tookey de chemin d’accès fichier&gt;</span><span class="sxs-lookup"><span data-stu-id="ba733-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path tookey file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-285">Cohérence</span><span class="sxs-lookup"><span data-stu-id="ba733-285">Consistency</span></span></td>
  <td><span data-ttu-id="ba733-286">Définir le niveau de cohérence hello par défaut pour le compte de hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-286">Set hello default consistency level for hello account.</span></span></td>
  <td><span data-ttu-id="ba733-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span><span class="sxs-lookup"><span data-stu-id="ba733-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="ba733-288">&lt;cohérence&gt;: valeur doit être un des éléments suivants de hello [niveaux de cohérence](consistency-levels.md): Session, fort, Eventual ou BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="ba733-288">&lt;consistency&gt;: Value must be one of hello following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="ba733-289">valeur par défaut de Hello est la Session.</span><span class="sxs-lookup"><span data-stu-id="ba733-289">hello default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="ba733-290">?</span><span class="sxs-lookup"><span data-stu-id="ba733-290">?</span></span></td>
  <td><span data-ttu-id="ba733-291">Afficher le message d’aide hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-291">Show hello help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="ba733-292">Différences entre hello Azure Cosmos DB émulateur et la base de données Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="ba733-292">Differences between hello Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="ba733-293">Étant donné que hello Azure Cosmos DB émulateur fournit un environnement émulé en cours d’exécution sur une station de travail de développement local, il existe quelques différences de fonctionnalités entre l’émulateur de hello et un compte de base de données Azure Cosmos dans le cloud de hello :</span><span class="sxs-lookup"><span data-stu-id="ba733-293">Because hello Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between hello emulator and an Azure Cosmos DB account in hello cloud:</span></span>

* <span data-ttu-id="ba733-294">Bonjour Azure Cosmos DB émulateur prend en charge un seul compte fixe et une clé principale connue.</span><span class="sxs-lookup"><span data-stu-id="ba733-294">hello Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="ba733-295">Régénération de la clé n’est pas possible dans hello Azure Cosmos DB émulateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-295">Key regeneration is not possible in hello Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="ba733-296">Hello Azure Cosmos DB émulateur n’est pas un service évolutif et ne prendra pas en charge un grand nombre de collections.</span><span class="sxs-lookup"><span data-stu-id="ba733-296">hello Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="ba733-297">Bonjour Azure Cosmos DB émulateur ne simule pas différents [niveaux de cohérence de base de données Azure Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="ba733-297">hello Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="ba733-298">Bonjour Azure Cosmos DB émulateur ne simule pas [multizone réplication](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="ba733-298">hello Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="ba733-299">Hello Azure Cosmos DB émulateur ne prend pas en charge les remplacements de quota de service hello qui sont disponibles dans le service de base de données Azure Cosmos hello (par exemple, les limites de taille de document, stockage de la collection partitionnée accrue).</span><span class="sxs-lookup"><span data-stu-id="ba733-299">hello Azure Cosmos DB Emulator does not support hello service quota overrides that are available in hello Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="ba733-300">Comme votre copie de hello Azure Cosmos DB émulateur peut-être pas des toodate avec les modifications les plus récentes avec le service de base de données Azure Cosmos hello hello, veuillez [Planificateur de capacité de base de données Azure Cosmos](https://www.documentdb.com/capacityplanner) tooaccurately estimation débit de production (RUs) besoins de votre application.</span><span class="sxs-lookup"><span data-stu-id="ba733-300">As your copy of hello Azure Cosmos DB Emulator might not be up toodate with hello most recent changes with hello Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) tooaccurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="ba733-301"><a id="set-partitioncount"></a>Modifier le nombre de hello de collections</span><span class="sxs-lookup"><span data-stu-id="ba733-301"><a id="set-partitioncount"></a>Change hello number of collections</span></span>

<span data-ttu-id="ba733-302">Par défaut, vous pouvez créer des collections de partitions uniques too25 ou 1 collection partitionnée à l’aide de hello Azure Cosmos DB émulateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-302">By default, you can create up too25 single partition collections, or 1 partitioned collection using hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="ba733-303">En modifiant hello **PartitionCount** valeur, vous pouvez créer des collections de partitions uniques too250 ou les collections partitionnées 10, ou n’importe quelle combinaison de hello deux qui ne dépasse pas 250 unique partitionne (où 1 partitionné collection = 25 collection de partition unique).</span><span class="sxs-lookup"><span data-stu-id="ba733-303">By modifying hello **PartitionCount** value, you can create up too250 single partition collections or 10 partitioned collections, or any combination of hello two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="ba733-304">Si vous essayez de toocreate une collection après que le nombre de partitions hello actuel a été dépassé, émulateur de hello lève une exception de ServiceUnavailable, avec hello message suivant.</span><span class="sxs-lookup"><span data-stu-id="ba733-304">If you attempt toocreate a collection after hello current partition count has been exceeded, hello emulator throws a ServiceUnavailable exception, with hello following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="ba733-305">nombre de hello toochange de toohello de collections disponibles Azure Cosmos DB émulateur, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="ba733-305">toochange hello number of collections available toohello Azure Cosmos DB Emulator, do hello following:</span></span>

1. <span data-ttu-id="ba733-306">Supprimer toutes les données Azure Cosmos DB émulateur locales en double-cliquant sur hello **Azure Cosmos DB émulateur** icône dans la barre d’état système hello, puis sur **réinitialiser les données en cours...** .</span><span class="sxs-lookup"><span data-stu-id="ba733-306">Delete all local Azure Cosmos DB Emulator data by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="ba733-307">Supprimez toutes les données de l’émulateur dans le dossier C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="ba733-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="ba733-308">Quittez toutes les instances ouvertes en cliquant sur hello **Azure Cosmos DB émulateur** icône dans la barre d’état système hello, puis sur **Exit**.</span><span class="sxs-lookup"><span data-stu-id="ba733-308">Exit all open instances by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="ba733-309">Il peut prendre une minute pour toutes les instances tooexit.</span><span class="sxs-lookup"><span data-stu-id="ba733-309">It may take a minute for all instances tooexit.</span></span>
4. <span data-ttu-id="ba733-310">Installer la version la plus récente de hello hello [Azure Cosmos DB émulateur](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="ba733-310">Install hello latest version of hello [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="ba733-311">Lancez l’émulateur hello avec hello PartitionCount indicateur en définissant une valeur < = 250.</span><span class="sxs-lookup"><span data-stu-id="ba733-311">Launch hello emulator with hello PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="ba733-312">Par exemple : `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="ba733-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ba733-313">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="ba733-313">Troubleshooting</span></span>

<span data-ttu-id="ba733-314">Utilisez hello suivant les conseils toohelp résoudre les problèmes que vous rencontrez avec l’émulateur de base de données Azure Cosmos hello :</span><span class="sxs-lookup"><span data-stu-id="ba733-314">Use hello following tips toohelp troubleshoot issues you encounter with hello Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="ba733-315">Si vous avez installé une nouvelle version de hello émulateur rencontrent des erreurs, vérifiez que vous réinitialisez vos données.</span><span class="sxs-lookup"><span data-stu-id="ba733-315">If you installed a new version of hello Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="ba733-316">Vous pouvez réinitialiser vos données, icône hello Azure Cosmos DB émulateur sur la barre d’état système hello, puis cliquez sur Réinitialiser les données en cours...</span><span class="sxs-lookup"><span data-stu-id="ba733-316">You can reset your data by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="ba733-317">Si cela ne résout pas les erreurs de hello, vous pouvez désinstaller et réinstaller l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-317">If that does not fix hello errors, you can uninstall and reinstall hello app.</span></span> <span data-ttu-id="ba733-318">Consultez [désinstaller l’émulateur local de hello](#uninstall) pour obtenir des instructions.</span><span class="sxs-lookup"><span data-stu-id="ba733-318">See [Uninstall hello local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="ba733-319">Si l’émulateur de base de données Azure Cosmos hello tombe en panne, collecter des fichiers de vidage à partir du dossier c:\Users\user_name\AppData\Local\CrashDumps les compresser et les joindre par courrier électronique tooan trop[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ba733-319">If hello Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="ba733-320">Si vous rencontrez des blocages dans CosmosDB.StartupEntryPoint.exe, exécutez hello de commande suivante à partir d’une invite de commandes administrateur :`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="ba733-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run hello following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="ba733-321">Si vous rencontrez un problème de connectivité, [collecter des fichiers de trace](#trace-files), de compresser et de les joindre par courrier électronique tooan trop[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="ba733-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="ba733-322">Si vous recevez un **Service indisponible** message, hello émulateur peut échouer la pile réseau tooinitialize hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-322">If you receive a **Service Unavailable** message, hello emulator might be failing tooinitialize hello network stack.</span></span> <span data-ttu-id="ba733-323">Vérification toosee si vous avez hello Pulse secure client ou Juniper réseaux client est installé, comme leurs pilotes de filtre réseau peuvent entraîner des problème de hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-323">Check toosee if you have hello Pulse secure client or Juniper networks client installed, as their network filter drivers may cause hello problem.</span></span> <span data-ttu-id="ba733-324">Désinstallation des pilotes de filtre réseau tiers généralement de résout le problème de hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-324">Uninstalling third party network filter drivers typically fixes hello issue.</span></span>

### <span data-ttu-id="ba733-325"><a id="trace-files"></a>Collecter les fichiers de trace</span><span class="sxs-lookup"><span data-stu-id="ba733-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="ba733-326">toocollect suivis, exécutez hello suivant les commandes à partir d’une invite de commandes d’administration de débogage :</span><span class="sxs-lookup"><span data-stu-id="ba733-326">toocollect debugging traces, run hello following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="ba733-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="ba733-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="ba733-328">Espion hello système toomake vraiment hello programme s’est arrêté, il peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="ba733-328">Watch hello system tray toomake sure hello program has shut down, it may take a minute.</span></span> <span data-ttu-id="ba733-329">Vous pouvez également cliquer sur **Exit** dans l’interface utilisateur de hello Azure Cosmos DB émulateur.</span><span class="sxs-lookup"><span data-stu-id="ba733-329">You can also just click **Exit** in hello Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="ba733-330">Reproduisez le problème de hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-330">Reproduce hello problem.</span></span> <span data-ttu-id="ba733-331">Si l’Explorateur de données ne fonctionne pas, vous devez uniquement toowait pour tooopen de navigateur hello pour erreur hello de toocatch quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="ba733-331">If Data Explorer is not working, you only need toowait for hello browser tooopen for a few seconds toocatch hello error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="ba733-332">Accédez trop`%ProgramFiles%\Azure Cosmos DB Emulator` et de trouver le fichier de docdbemulator_000001.etl hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-332">Navigate too`%ProgramFiles%\Azure Cosmos DB Emulator` and find hello docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="ba733-333">Envoyer le fichier .etl de hello, ainsi que les étapes de reproduction trop[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="ba733-333">Send hello .etl file along with repro steps too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="ba733-334"><a id="uninstall"></a>Désinstaller hello émulateur local</span><span class="sxs-lookup"><span data-stu-id="ba733-334"><a id="uninstall"></a>Uninstall hello local Emulator</span></span>

1. <span data-ttu-id="ba733-335">Quittez toutes les instances ouvertes de hello émulateur local, icône hello Azure Cosmos DB émulateur sur la barre d’état système hello, puis cliquez sur Quitter.</span><span class="sxs-lookup"><span data-stu-id="ba733-335">Exit all open instances of hello local Emulator by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Exit.</span></span> <span data-ttu-id="ba733-336">Il peut prendre une minute pour toutes les instances tooexit.</span><span class="sxs-lookup"><span data-stu-id="ba733-336">It may take a minute for all instances tooexit.</span></span>
2. <span data-ttu-id="ba733-337">Dans la zone de recherche de Windows hello, tapez **applications & fonctionnalités** , puis cliquez sur hello **caractéristiques (paramètres système) et les applications** résultat.</span><span class="sxs-lookup"><span data-stu-id="ba733-337">In hello Windows search box, type **Apps & features** and click on hello **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="ba733-338">Dans la liste de hello des applications, faites défiler trop**Azure Cosmos DB émulateur**, sélectionnez-la, cliquez sur **désinstallation**, puis confirmer, cliquez sur **désinstallation** à nouveau.</span><span class="sxs-lookup"><span data-stu-id="ba733-338">In hello list of apps, scroll too**Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="ba733-339">Lors de l’application hello est désinstallée, accédez à tooC:\Users\<utilisateur > \AppData\Local\CosmosDBEmulator et supprimer le dossier hello.</span><span class="sxs-lookup"><span data-stu-id="ba733-339">When hello app is uninstalled, navigate tooC:\Users\<user>\AppData\Local\CosmosDBEmulator and delete hello folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ba733-340">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba733-340">Next steps</span></span>

<span data-ttu-id="ba733-341">Dans ce didacticiel, vous avez effectué les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="ba733-341">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ba733-342">Installé hello émulateur local</span><span class="sxs-lookup"><span data-stu-id="ba733-342">Installed hello local Emulator</span></span>
> * <span data-ttu-id="ba733-343">RAND hello émulateur sur Docker pour Windows</span><span class="sxs-lookup"><span data-stu-id="ba733-343">Rand hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="ba733-344">Authentifié des requêtes</span><span class="sxs-lookup"><span data-stu-id="ba733-344">Authenticated requests</span></span>
> * <span data-ttu-id="ba733-345">Utilisé hello Explorateur de données dans l’émulateur de hello</span><span class="sxs-lookup"><span data-stu-id="ba733-345">Used hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="ba733-346">Exporté des certificats SSL</span><span class="sxs-lookup"><span data-stu-id="ba733-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="ba733-347">Appelée hello émulateur à partir de la ligne de commande hello</span><span class="sxs-lookup"><span data-stu-id="ba733-347">Called hello Emulator from hello command line</span></span>
> * <span data-ttu-id="ba733-348">Collecté les fichiers de trace</span><span class="sxs-lookup"><span data-stu-id="ba733-348">Collected trace files</span></span>

<span data-ttu-id="ba733-349">Dans ce didacticiel, vous avez appris comment toouse hello émulateur local pour le développement local gratuit.</span><span class="sxs-lookup"><span data-stu-id="ba733-349">In this tutorial, you've learned how toouse hello local Emulator for free local development.</span></span> <span data-ttu-id="ba733-350">Vous pouvez maintenant continuer le didacticiel suivant de toohello et savoir comment les certificats SSL de l’émulateur tooexport.</span><span class="sxs-lookup"><span data-stu-id="ba733-350">You can now proceed toohello next tutorial and learn how tooexport Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="ba733-351">Exporter des certificats d’émulateur de base de données Azure Cosmos hello</span><span class="sxs-lookup"><span data-stu-id="ba733-351">Export hello Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
