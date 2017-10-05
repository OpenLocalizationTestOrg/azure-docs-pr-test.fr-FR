---
title: "Développement local avec l’émulateur Azure Cosmos DB | Microsoft Docs"
description: "L’émulateur Azure Cosmos DB vous permet de développer et de tester votre application localement, sans créer d’abonnement Azure et sans frais."
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
ms.openlocfilehash: a0f6a845a345ebd4ef0a58abf4934ce400103109
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="beae4-104">Utilisation de l’émulateur Azure Cosmos DB pour le développement local et le test</span><span class="sxs-lookup"><span data-stu-id="beae4-104">Use the Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="beae4-105"><strong>Fichiers binaires</strong></span><span class="sxs-lookup"><span data-stu-id="beae4-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="beae4-106">Télécharger MSI</span><span class="sxs-lookup"><span data-stu-id="beae4-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="beae4-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="beae4-108">Docker Hub</span><span class="sxs-lookup"><span data-stu-id="beae4-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-109"><strong>Source Docker</strong></span><span class="sxs-lookup"><span data-stu-id="beae4-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="beae4-110">Github</span><span class="sxs-lookup"><span data-stu-id="beae4-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="beae4-111">L’émulateur Azure Cosmos DB fournit un environnement local qui émule le service Azure Cosmos DB à des fins de développement.</span><span class="sxs-lookup"><span data-stu-id="beae4-111">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="beae4-112">L’émulateur Azure Cosmos DB vous permet de développer et de tester votre application localement, sans créer d’abonnement Azure et sans frais.</span><span class="sxs-lookup"><span data-stu-id="beae4-112">Using the Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="beae4-113">Lorsque vous êtes satisfait du fonctionnement de votre application dans l’émulateur Azure Cosmos DB, vous pouvez commencer à utiliser un compte Azure Cosmos DB dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="beae4-113">When you're satisfied with how your application is working in the Azure Cosmos DB Emulator, you can switch to using an Azure Cosmos DB account in the cloud.</span></span>

<span data-ttu-id="beae4-114">Cet article décrit les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="beae4-114">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="beae4-115">Installation de l’émulateur</span><span class="sxs-lookup"><span data-stu-id="beae4-115">Installing the Emulator</span></span>
> * <span data-ttu-id="beae4-116">Exécution de l’émulateur sur Docker pour Windows</span><span class="sxs-lookup"><span data-stu-id="beae4-116">Running the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="beae4-117">Authentification des demandes</span><span class="sxs-lookup"><span data-stu-id="beae4-117">Authenticating requests</span></span>
> * <span data-ttu-id="beae4-118">Utilisation de l’Explorateur de données dans l’émulateur</span><span class="sxs-lookup"><span data-stu-id="beae4-118">Using the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="beae4-119">Exportation de certificats SSL</span><span class="sxs-lookup"><span data-stu-id="beae4-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="beae4-120">Appel de l’émulateur à partir de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="beae4-120">Calling the Emulator from the command line</span></span>
> * <span data-ttu-id="beae4-121">Collecte des fichiers de trace</span><span class="sxs-lookup"><span data-stu-id="beae4-121">Collecting trace files</span></span>

<span data-ttu-id="beae4-122">Nous vous recommandons de commencer par visionner la vidéo suivante, où Kirill Gavrylyuk montre comment prendre en main l’émulateur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-122">We recommend getting started by watching the following video, where Kirill Gavrylyuk shows how to get started with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="beae4-123">Notez que la vidéo fait référence à l’émulateur en tant qu’émulateur de DocumentDB, mais que l’outil proprement dit a été renommé Émulateur d’Azure Cosmos DB depuis l’enregistrement de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="beae4-123">Note that the video refers to the emulator as the DocumentDB Emulator, but the tool itself has been renamed the Azure Cosmos DB Emulator since taping the video.</span></span> <span data-ttu-id="beae4-124">Toutes les informations contenues dans la vidéo restent exactes pour l’émulateur d’Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-124">All information in the video is still accurate for the Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-the-emulator-works"></a><span data-ttu-id="beae4-125">Fonctionnement de l’émulateur</span><span class="sxs-lookup"><span data-stu-id="beae4-125">How the Emulator works</span></span>
<span data-ttu-id="beae4-126">L’émulateur Azure Cosmos DB fournit une émulation haute fidélité du service Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-126">The Azure Cosmos DB Emulator provides a high-fidelity emulation of the Azure Cosmos DB service.</span></span> <span data-ttu-id="beae4-127">Il prend en charge les mêmes fonctionnalités qu’Azure Cosmos DB, notamment la prise en charge de la création et de l’interrogation des documents JSON, la configuration et la mise à l’échelle des collections, et l’exécution des procédures stockées et des déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="beae4-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="beae4-128">Vous pouvez développer et tester des applications à l’aide de l’émulateur Azure Cosmos DB et les déployer vers Azure à l’échelle mondiale en apportant une seule modification à la configuration du point de terminaison de connexion pour Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-128">You can develop and test applications using the Azure Cosmos DB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="beae4-129">Nous avons créé une émulation locale haute fidélité du service Azure Cosmos DB réel, mais l’implémentation de l’émulateur Azure Cosmos DB est différente de celle du service.</span><span class="sxs-lookup"><span data-stu-id="beae4-129">While we created a high-fidelity local emulation of the actual Azure Cosmos DB service, the implementation of the Azure Cosmos DB Emulator is different than that of the service.</span></span> <span data-ttu-id="beae4-130">Par exemple, l’émulateur Azure Cosmos DB utilise les composants du système d’exploitation standard, notamment le système de fichiers local pour la persistance, et la pile de protocole HTTPS pour la connectivité.</span><span class="sxs-lookup"><span data-stu-id="beae4-130">For example, the Azure Cosmos DB Emulator uses standard OS components such as the local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="beae4-131">Cela signifie que certaines fonctionnalités qui s’appuient sur l’infrastructure Azure, comme la réplication globale, la latence en quelques millisecondes pour les lectures/écritures et les niveaux de cohérence ajustables ne sont pas disponibles via l’émulateur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via the Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="beae4-132">À ce stade l’Explorateur de données dans l’émulateur prend uniquement en charge la création de collections d’API DocumentDB et de collections MongoDB.</span><span class="sxs-lookup"><span data-stu-id="beae4-132">At this time the Data Explorer in the emulator only supports the creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="beae4-133">L’Explorateur de données dans l’émulateur ne prend actuellement pas en charge la création de tables et les graphiques.</span><span class="sxs-lookup"><span data-stu-id="beae4-133">The Data Explorer in the emulator does not currently support the creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="beae4-134">Conditions requises pour le système</span><span class="sxs-lookup"><span data-stu-id="beae4-134">System requirements</span></span>
<span data-ttu-id="beae4-135">L’émulateur Azure Cosmos DB nécessite la configuration matérielle et logicielle suivante :</span><span class="sxs-lookup"><span data-stu-id="beae4-135">The Azure Cosmos DB Emulator has the following hardware and software requirements:</span></span>

* <span data-ttu-id="beae4-136">Configuration logicielle requise</span><span class="sxs-lookup"><span data-stu-id="beae4-136">Software requirements</span></span>
  * <span data-ttu-id="beae4-137">Windows Server 2012 R2, Windows Server 2016 ou Windows 10</span><span class="sxs-lookup"><span data-stu-id="beae4-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="beae4-138">Conditions matérielles minimales requises</span><span class="sxs-lookup"><span data-stu-id="beae4-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="beae4-139">2 Go de RAM</span><span class="sxs-lookup"><span data-stu-id="beae4-139">2 GB RAM</span></span>
  * <span data-ttu-id="beae4-140">10 Go d’espace disque disponible</span><span class="sxs-lookup"><span data-stu-id="beae4-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="beae4-141">Installation</span><span class="sxs-lookup"><span data-stu-id="beae4-141">Installation</span></span>
<span data-ttu-id="beae4-142">Vous pouvez télécharger et installer l’émulateur Azure Cosmos DB à partir du [Centre de téléchargement Microsoft](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="beae4-142">You can download and install the Azure Cosmos DB Emulator from the [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="beae4-143">Pour installer, configurer et exécuter l’émulateur Azure Cosmos DB, vous devez disposer de privilèges d’administrateur sur l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="beae4-143">To install, configure, and run the Azure Cosmos DB Emulator, you must have administrative privileges on the computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="beae4-144">Exécution de Docker pour Windows</span><span class="sxs-lookup"><span data-stu-id="beae4-144">Running on Docker for Windows</span></span>

<span data-ttu-id="beae4-145">L’émulateur Azure Cosmos DB peut être exécuté sur Docker pour Windows.</span><span class="sxs-lookup"><span data-stu-id="beae4-145">The Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="beae4-146">L’émulateur ne fonctionne pas sur Docker pour Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="beae4-146">The Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="beae4-147">Une fois que [Docker pour Windows](https://www.docker.com/docker-windows) est installé, vous pouvez extraire l’image de l’émulateur à partir de Docker Hub en exécutant la commande suivante depuis votre interpréteur de commandes favori (cmd.exe, PowerShell, etc.).</span><span class="sxs-lookup"><span data-stu-id="beae4-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull the Emulator image from Docker Hub by running the following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="beae4-148">Pour démarrer l’image, exécutez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="beae4-148">To start the image, run the following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="beae4-149">La réponse ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="beae4-149">The response looks similar to the following:</span></span>

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import the SSL certificate from an administrator command prompt on the host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

<span data-ttu-id="beae4-150">Si vous fermez l’interpréteur de commandes interactif une fois que l’émulateur a été démarré, le conteneur de l’émulateur s’éteint.</span><span class="sxs-lookup"><span data-stu-id="beae4-150">Closing the interactive shell once the Emulator has been started will shutdown the Emulator’s container.</span></span>

<span data-ttu-id="beae4-151">Utilisez le point de terminaison et la clé principale dans la réponse de votre client et importez le certificat SSL dans votre hôte.</span><span class="sxs-lookup"><span data-stu-id="beae4-151">Use the endpoint and master key in from the response in your client and import the SSL certificate into your host.</span></span> <span data-ttu-id="beae4-152">Pour importer le certificat SSL, procédez comme suit à partir d’une invite de commandes administrateur :</span><span class="sxs-lookup"><span data-stu-id="beae4-152">To import the SSL certificate, do the following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-the-emulator"></a><span data-ttu-id="beae4-153">Démarrer l’émulateur</span><span class="sxs-lookup"><span data-stu-id="beae4-153">Start the Emulator</span></span>

<span data-ttu-id="beae4-154">Pour démarrer l’émulateur Azure Cosmos DB, sélectionnez le bouton Démarrer ou appuyez sur la touche Windows.</span><span class="sxs-lookup"><span data-stu-id="beae4-154">To start the Azure Cosmos DB Emulator, select the Start button or press the Windows key.</span></span> <span data-ttu-id="beae4-155">Commencez à taper **Émulateur Azure Cosmos DB**, puis sélectionnez l’émulateur dans la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="beae4-155">Begin typing **Azure Cosmos DB Emulator**, and select the emulator from the list of applications.</span></span> 

![Sélectionnez le bouton Démarrer ou appuyez sur la touche Windows, commencez à taper **Azure Cosmos DB**, puis sélectionnez l’émulateur dans la liste des applications](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="beae4-157">Lorsque l’émulateur est en cours d’exécution, une icône est affichée dans la zone de notification de la barre des tâches Windows.</span><span class="sxs-lookup"><span data-stu-id="beae4-157">When the emulator is running, you'll see an icon in the Windows taskbar notification area.</span></span> ![Notification dans la barre des tâches de l'émulateur local Azure Cosmos DB](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="beae4-159">L’émulateur Azure Cosmos DB s’exécute par défaut sur l’ordinateur local (« localhost ») et écoute sur le port 8081.</span><span class="sxs-lookup"><span data-stu-id="beae4-159">The Azure Cosmos DB Emulator by default runs on the local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="beae4-160">L’émulateur Azure Cosmos DB est installé par défaut dans le répertoire `C:\Program Files\Azure Cosmos DB Emulator`.</span><span class="sxs-lookup"><span data-stu-id="beae4-160">The Azure Cosmos DB Emulator is installed by default to the `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="beae4-161">Vous pouvez également démarrer et arrêter l’émulateur à partir de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="beae4-161">You can also start and stop the emulator from the command-line.</span></span> <span data-ttu-id="beae4-162">Pour plus d’informations, consultez la section [Référence de l’outil en ligne de commande](#command-line).</span><span class="sxs-lookup"><span data-stu-id="beae4-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="beae4-163">Démarrer l’Explorateur de données</span><span class="sxs-lookup"><span data-stu-id="beae4-163">Start Data Explorer</span></span>

<span data-ttu-id="beae4-164">Au démarrage de l’émulateur Azure Cosmos DB, l’Explorateur de données Azure Cosmos DB s’ouvre automatiquement dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="beae4-164">When the Azure Cosmos DB emulator launches it will automatically open the Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="beae4-165">L’adresse apparaît sous la forme [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="beae4-165">The address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="beae4-166">Si vous fermez l’explorateur et que vous souhaitez le rouvrir ultérieurement, vous pouvez ouvrir l’URL dans votre navigateur ou la lancer à partir de l’émulateur Azure Cosmos DB dans l’icône de la barre d’état système Windows, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="beae4-166">If you close the explorer and would like to re-open it later, you can either open the URL in your browser or launch it from the Azure Cosmos DB Emulator in the Windows Tray Icon as shown below.</span></span>

![Lanceur de l’Explorateur de données de l’émulateur local Azure Cosmos DB](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="beae4-168">Recherche de mises à jour</span><span class="sxs-lookup"><span data-stu-id="beae4-168">Checking for updates</span></span>
<span data-ttu-id="beae4-169">L’Explorateur de données indique si une nouvelle mise à jour est disponible en téléchargement.</span><span class="sxs-lookup"><span data-stu-id="beae4-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="beae4-170">Il n’est pas garanti que vous puissiez accéder aux données créées dans une version de l’émulateur Azure Cosmos DB à partir d’une autre version.</span><span class="sxs-lookup"><span data-stu-id="beae4-170">Data created in one version of the Azure Cosmos DB Emulator is not guaranteed to be accessible when using a different version.</span></span> <span data-ttu-id="beae4-171">Si vous devez rendre vos données persistantes à long terme, nous vous recommandons de stocker ces données dans un compte Azure Cosmos DB plutôt que dans l’émulateur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-171">If you need to persist your data for the long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in the Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="beae4-172">Authentification des demandes</span><span class="sxs-lookup"><span data-stu-id="beae4-172">Authenticating requests</span></span>
<span data-ttu-id="beae4-173">Tout comme avec Azure Cosmos DB dans le cloud, chaque demande que vous effectuez auprès de l’émulateur Azure Cosmos DB doit être authentifiée.</span><span class="sxs-lookup"><span data-stu-id="beae4-173">Just as with Azure Cosmos DB in the cloud, every request that you make against the Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="beae4-174">L’émulateur Azure Cosmos DB prend en charge uniquement un compte fixe et une clé d’authentification connue pour l’authentification de la clé principale.</span><span class="sxs-lookup"><span data-stu-id="beae4-174">The Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="beae4-175">Ce compte et cette clé sont les seules informations d’identification autorisées pour une utilisation avec l’émulateur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-175">This account and key are the only credentials permitted for use with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="beae4-176">Il s'agit de :</span><span class="sxs-lookup"><span data-stu-id="beae4-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="beae4-177">La clé principale prise en charge par l’émulateur Azure Cosmos DB est destinée à être utilisée uniquement avec l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="beae4-177">The master key supported by the Azure Cosmos DB Emulator is intended for use only with the emulator.</span></span> <span data-ttu-id="beae4-178">Vous ne pouvez pas utiliser votre compte et votre clé Azure Cosmos DB de production avec l’émulateur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-178">You cannot use your production Azure Cosmos DB account and key with the Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="beae4-179">Si vous avez démarré l’émulateur avec l’option /Key, utilisez la clé générée au lieu de « C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw== »</span><span class="sxs-lookup"><span data-stu-id="beae4-179">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="beae4-180">En outre, comme pour le service Azure Cosmos DB, l’émulateur Azure Cosmos DB prend en charge uniquement une communication sécurisée via SSL.</span><span class="sxs-lookup"><span data-stu-id="beae4-180">Additionally, just as the Azure Cosmos DB service, the Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-the-emulator-on-a-local-network"></a><span data-ttu-id="beae4-181">Exécution de l’émulateur sur un réseau local</span><span class="sxs-lookup"><span data-stu-id="beae4-181">Running the emulator on a local network</span></span>

<span data-ttu-id="beae4-182">Vous pouvez exécuter l’émulateur sur un réseau local.</span><span class="sxs-lookup"><span data-stu-id="beae4-182">You can run the emulator on a local network.</span></span> <span data-ttu-id="beae4-183">Pour activer l’accès réseau, spécifiez l’option /AllowNetworkAccess à la [ligne de commande](#command-line-syntax) qui nécessite également que vous indiquiez /KEY = key_string ou/keyfile = file_name.</span><span class="sxs-lookup"><span data-stu-id="beae4-183">To enable network access, specify the /AllowNetworkAccess option at the [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="beae4-184">Vous pouvez initialement utiliser /GenKeyFile = nom_fichier pour générer un fichier avec une clé aléatoire.</span><span class="sxs-lookup"><span data-stu-id="beae4-184">You can use /GenKeyFile=file_name to generate a file with a random key upfront.</span></span>  <span data-ttu-id="beae4-185">Passez ensuite à/keyfile = nom_fichier ou/Key = contents_of_file.</span><span class="sxs-lookup"><span data-stu-id="beae4-185">Then you can pass that to /KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="beae4-186">Pour activer l’accès réseau pour la première fois, l’utilisateur doit arrêter l’émulateur et supprimer son répertoire de données (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="beae4-186">To enable network access for the first time the user should shutdown the emulator and delete the emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-the-emulator"></a><span data-ttu-id="beae4-187">Développement avec l’émulateur</span><span class="sxs-lookup"><span data-stu-id="beae4-187">Developing with the Emulator</span></span>
<span data-ttu-id="beae4-188">Une fois que l’émulateur Azure Cosmos DB est exécuté sur votre bureau, vous pouvez utiliser n’importe quel [SDK Azure Cosmos DB](documentdb-sdk-dotnet.md) pris en charge ou [l’API REST Azure Cosmos DB](/rest/api/documentdb/) pour interagir avec lui.</span><span class="sxs-lookup"><span data-stu-id="beae4-188">Once you have the Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or the [Azure Cosmos DB REST API](/rest/api/documentdb/) to interact with the Emulator.</span></span> <span data-ttu-id="beae4-189">L’émulateur Azure Cosmos DB inclut également un Explorateur de données intégré qui vous permet de créer des collections pour les API DocumentDB et MongoDB, ainsi que d’afficher et de modifier des documents sans avoir à écrire de code.</span><span class="sxs-lookup"><span data-stu-id="beae4-189">The Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for the DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect to the Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="beae4-190">Si vous utilisez la [prise en charge du protocole Azure Cosmos DB pour MongoDB](mongodb-introduction.md), utilisez la chaîne de connexion suivante :</span><span class="sxs-lookup"><span data-stu-id="beae4-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use the following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="beae4-191">Vous pouvez utiliser les outils existants comme [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) pour vous connecter à l’émulateur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="beae4-192">Vous pouvez également migrer des données entre l’émulateur Azure Cosmos DB et le service Azure Cosmos DB à l’aide de [l’outil de migration de données Azure Cosmos DB](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="beae4-192">You can also migrate data between the Azure Cosmos DB Emulator and the Azure Cosmos DB service using the [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="beae4-193">Si vous avez démarré l’émulateur avec l’option /Key, utilisez la clé générée au lieu de « C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw== »</span><span class="sxs-lookup"><span data-stu-id="beae4-193">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="beae4-194">À l’aide de l’émulateur Azure Cosmos DB, vous pouvez, par défaut, créer jusqu’à 25 collections à partition unique ou 1 collection partitionnée.</span><span class="sxs-lookup"><span data-stu-id="beae4-194">Using the Azure Cosmos DB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="beae4-195">Pour plus d’informations sur la modification de cette valeur, voir la section relative à la [définition de la valeur PartitionCount](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="beae4-195">For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-the-ssl-certificate"></a><span data-ttu-id="beae4-196">Exporter le certificat SSL</span><span class="sxs-lookup"><span data-stu-id="beae4-196">Export the SSL certificate</span></span>

<span data-ttu-id="beae4-197">Les langages .NET et le runtime utilisent le magasin de certificats Windows pour se connecter en toute sécurité à l’émulateur local Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-197">.NET languages and runtime use the Windows Certificate Store to securely connect to the Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="beae4-198">D’autres langages ont leur propre méthode de gestion et de l’utilisation des certificats.</span><span class="sxs-lookup"><span data-stu-id="beae4-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="beae4-199">Java utilise son propre [magasin de certificats](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html), tandis que Python utilise des [wrappers de socket](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="beae4-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="beae4-200">Pour obtenir un certificat à utiliser avec les langages et les runtimes qui ne s’intègrent pas au magasin de certificats Windows, vous devrez l'exporter à l’aide du Gestionnaire de certificats Windows.</span><span class="sxs-lookup"><span data-stu-id="beae4-200">In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store you will need to export it using the Windows Certificate Manager.</span></span> <span data-ttu-id="beae4-201">Vous pouvez le démarrer en exécutant le fichier certlm.msc ou suivre les instructions étape par étape de la publication [Exporter les certificats de l’émulateur Azure Cosmos DB](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="beae4-201">You can start it by running certlm.msc or follow the step by step instructions in [Export the Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="beae4-202">Une fois le certificat en cours d’exécution, ouvrez les certificats personnels comme indiqué ci-dessous et exportez le certificat avec le nom convivial "DocumentDBEmulatorCertificate" en tant que fichier X.509 (.cer) codé en Base 64.</span><span class="sxs-lookup"><span data-stu-id="beae4-202">Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Certificat SSL de l’émulateur local Azure Cosmos DB](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="beae4-204">Le certificat X.509 peut être importé dans le magasin de certificats Java en suivant les instructions de la publication [Ajout d’un certificat au magasin de certificats d’autorité de certification Java](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="beae4-204">The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="beae4-205">Une fois le certificat importé dans le magasin de certificats, les applications Java et MongoDB peuvent se connecter à l’émulateur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-205">Once the certificate is imported into the certificate store, Java and MongoDB applications will be able to connect to the Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="beae4-206">Lors de la connexion à l’émulateur à partir des Kits de développement logiciel (SDK) Python et Node.js, la vérification SSL est désactivée.</span><span class="sxs-lookup"><span data-stu-id="beae4-206">When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="beae4-207"><a id="command-line"></a>Référence sur l’outil en ligne de commande</span><span class="sxs-lookup"><span data-stu-id="beae4-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="beae4-208">À partir de l’emplacement d’installation, vous pouvez utiliser la ligne de commande pour démarrer et arrêter l’émulateur, configurer les options et effectuer d’autres opérations.</span><span class="sxs-lookup"><span data-stu-id="beae4-208">From the installation location, you can use the command-line to start and stop the emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="beae4-209">Syntaxe de ligne de commande</span><span class="sxs-lookup"><span data-stu-id="beae4-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="beae4-210">Pour afficher la liste des options, tapez `CosmosDB.Emulator.exe /?` dans l’invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="beae4-210">To view the list of options, type `CosmosDB.Emulator.exe /?` at the command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="beae4-211"><strong>Option</strong></span><span class="sxs-lookup"><span data-stu-id="beae4-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="beae4-212"><strong>Description</strong></span><span class="sxs-lookup"><span data-stu-id="beae4-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="beae4-213"><strong>Commande</strong></span><span class="sxs-lookup"><span data-stu-id="beae4-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="beae4-214"><strong>Arguments</strong></span><span class="sxs-lookup"><span data-stu-id="beae4-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-215">[aucun argument]</span><span class="sxs-lookup"><span data-stu-id="beae4-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="beae4-216">Démarre l’émulateur Azure Cosmos DB avec des paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="beae4-216">Starts up the Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="beae4-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="beae4-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-218">[Aide]</span><span class="sxs-lookup"><span data-stu-id="beae4-218">[Help]</span></span></td>
  <td><span data-ttu-id="beae4-219">Affiche la liste des arguments de ligne de commande pris en charge.</span><span class="sxs-lookup"><span data-stu-id="beae4-219">Displays the list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="beae4-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="beae4-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-221">Shutdown</span><span class="sxs-lookup"><span data-stu-id="beae4-221">Shutdown</span></span></td>
  <td><span data-ttu-id="beae4-222">Arrête l’émulateur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-222">Shuts down the Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="beae4-223">CosmosDB.Emulator.exe /Shutdown</span><span class="sxs-lookup"><span data-stu-id="beae4-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-224">DataPath</span><span class="sxs-lookup"><span data-stu-id="beae4-224">DataPath</span></span></td>
  <td><span data-ttu-id="beae4-225">Spécifie le chemin d’accès dans lequel stocker les fichiers de données.</span><span class="sxs-lookup"><span data-stu-id="beae4-225">Specifies the path in which to store data files.</span></span> <span data-ttu-id="beae4-226">La valeur par défaut est %LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="beae4-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="beae4-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span><span class="sxs-lookup"><span data-stu-id="beae4-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="beae4-228">&lt;datapath&gt; : un chemin accessible</span><span class="sxs-lookup"><span data-stu-id="beae4-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-229">Port</span><span class="sxs-lookup"><span data-stu-id="beae4-229">Port</span></span></td>
  <td><span data-ttu-id="beae4-230">Spécifie le numéro de port à utiliser pour l'émulateur.</span><span class="sxs-lookup"><span data-stu-id="beae4-230">Specifies the port number to use for the emulator.</span></span>  <span data-ttu-id="beae4-231">La valeur par défaut est 8081.</span><span class="sxs-lookup"><span data-stu-id="beae4-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="beae4-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span><span class="sxs-lookup"><span data-stu-id="beae4-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="beae4-233">&lt;port&gt; : numéro de port unique</span><span class="sxs-lookup"><span data-stu-id="beae4-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="beae4-234">MongoPort</span></span></td>
  <td><span data-ttu-id="beae4-235">Spécifie le numéro de port à utiliser pour l'API de compatibilité MongoDB.</span><span class="sxs-lookup"><span data-stu-id="beae4-235">Specifies the port number to use for MongoDB compatibility API.</span></span> <span data-ttu-id="beae4-236">La valeur par défaut est 10255.</span><span class="sxs-lookup"><span data-stu-id="beae4-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="beae4-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="beae4-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="beae4-238">&lt;mongoport&gt; : numéro de port unique</span><span class="sxs-lookup"><span data-stu-id="beae4-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="beae4-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="beae4-240">Spécifie les ports à utiliser pour une connectivité directe.</span><span class="sxs-lookup"><span data-stu-id="beae4-240">Specifies the ports to use for direct connectivity.</span></span> <span data-ttu-id="beae4-241">Les valeurs par défaut sont 10251,10252,10253,10254.</span><span class="sxs-lookup"><span data-stu-id="beae4-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="beae4-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="beae4-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="beae4-243">&lt;directports&gt; : liste séparée par des virgules de 4 ports</span><span class="sxs-lookup"><span data-stu-id="beae4-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-244">Clé</span><span class="sxs-lookup"><span data-stu-id="beae4-244">Key</span></span></td>
  <td><span data-ttu-id="beae4-245">Clé d’autorisation pour l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="beae4-245">Authorization key for the emulator.</span></span> <span data-ttu-id="beae4-246">La clé doit être le codage en base 64 d’un vecteur de 64 octets.</span><span class="sxs-lookup"><span data-stu-id="beae4-246">Key must be the base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="beae4-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span><span class="sxs-lookup"><span data-stu-id="beae4-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="beae4-248">&lt;clé&gt; : la clé doit être le codage en base 64 d’un vecteur de 64 octets</span><span class="sxs-lookup"><span data-stu-id="beae4-248">&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="beae4-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="beae4-250">Spécifie que le comportement de limitation de taux de demandes est activé.</span><span class="sxs-lookup"><span data-stu-id="beae4-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="beae4-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="beae4-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="beae4-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="beae4-253">Spécifie que le comportement de limitation de taux de demandes est désactivé.</span><span class="sxs-lookup"><span data-stu-id="beae4-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="beae4-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="beae4-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="beae4-255">NoUI</span></span></td>
  <td><span data-ttu-id="beae4-256">Ne pas afficher l’interface utilisateur de l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="beae4-256">Do not show the emulator user interface.</span></span></td>
  <td><span data-ttu-id="beae4-257">CosmosDB.Emulator.exe /NoUI</span><span class="sxs-lookup"><span data-stu-id="beae4-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="beae4-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="beae4-259">Ne pas afficher l’Explorateur de documents au démarrage.</span><span class="sxs-lookup"><span data-stu-id="beae4-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="beae4-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="beae4-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="beae4-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="beae4-262">Spécifie le nombre maximal de collections partitionnées.</span><span class="sxs-lookup"><span data-stu-id="beae4-262">Specifies the maximum number of partitioned collections.</span></span> <span data-ttu-id="beae4-263">Pour plus d’informations, voir la section [Modification du nombre de collections](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="beae4-263">See [Change the number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="beae4-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="beae4-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="beae4-265">&lt;partitioncount&gt; : nombre maximal autorisé de collections à partition unique.</span><span class="sxs-lookup"><span data-stu-id="beae4-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="beae4-266">Valeur par défaut : 25.</span><span class="sxs-lookup"><span data-stu-id="beae4-266">Default is 25.</span></span> <span data-ttu-id="beae4-267">Valeur maximale autorisée : 250.</span><span class="sxs-lookup"><span data-stu-id="beae4-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="beae4-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="beae4-269">Spécifie le nombre par défaut des partitions pour une collection partitionnée.</span><span class="sxs-lookup"><span data-stu-id="beae4-269">Specifies the default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="beae4-270">CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="beae4-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="beae4-271">&lt;defaultpartitioncount&gt; La valeur par défaut est 25.</span><span class="sxs-lookup"><span data-stu-id="beae4-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="beae4-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="beae4-273">Permet d’accéder à l’émulateur sur un réseau.</span><span class="sxs-lookup"><span data-stu-id="beae4-273">Enables access to the emulator over a network.</span></span> <span data-ttu-id="beae4-274">Vous devez également passer/Key =&lt;key_string&gt; ou/keyfile =&lt;nom_fichier&gt; pour activer l’accès réseau.</span><span class="sxs-lookup"><span data-stu-id="beae4-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; to enable network access.</span></span></td>
  <td><span data-ttu-id="beae4-275">CosmosDB.Emulator.exe AllowNetworkAccess /Key =&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="beae4-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="beae4-276">ou</span><span class="sxs-lookup"><span data-stu-id="beae4-276">or</span></span><br><br><span data-ttu-id="beae4-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span><span class="sxs-lookup"><span data-stu-id="beae4-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="beae4-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="beae4-279">Ne pas ajuster les règles de pare-feu lors de l’utilisation de /AllowNetworkAccess.</span><span class="sxs-lookup"><span data-stu-id="beae4-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="beae4-280">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="beae4-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="beae4-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="beae4-282">Générer une nouvelle clé d’autorisation et Générer une nouvelle clé d’autorisation et l’enregistrer dans le fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="beae4-282">Generate a new authorization key and save to the specified file.</span></span> <span data-ttu-id="beae4-283">La clé générée peut être utilisée avec les options /Key or /KeyFile.</span><span class="sxs-lookup"><span data-stu-id="beae4-283">The generated key can be used with the /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="beae4-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;chemin du fichier de clé&gt;</span><span class="sxs-lookup"><span data-stu-id="beae4-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path to key file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-285">Cohérence</span><span class="sxs-lookup"><span data-stu-id="beae4-285">Consistency</span></span></td>
  <td><span data-ttu-id="beae4-286">Définir le niveau de cohérence par défaut pour le compte.</span><span class="sxs-lookup"><span data-stu-id="beae4-286">Set the default consistency level for the account.</span></span></td>
  <td><span data-ttu-id="beae4-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span><span class="sxs-lookup"><span data-stu-id="beae4-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="beae4-288">&lt;cohérence&gt; : la valeur doit être l’un des [niveaux de cohérence](consistency-levels.md) proposés (Session, Strong, Eventual ou BoundedStaleness).</span><span class="sxs-lookup"><span data-stu-id="beae4-288">&lt;consistency&gt;: Value must be one of the following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="beae4-289">La valeur par défaut est Session.</span><span class="sxs-lookup"><span data-stu-id="beae4-289">The default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="beae4-290">?</span><span class="sxs-lookup"><span data-stu-id="beae4-290">?</span></span></td>
  <td><span data-ttu-id="beae4-291">Afficher le message d’aide.</span><span class="sxs-lookup"><span data-stu-id="beae4-291">Show the help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-the-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="beae4-292">Différences entre l’émulateur Azure Cosmos DB et Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="beae4-292">Differences between the Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="beae4-293">L’émulateur Azure Cosmos DB étant un environnement émulé exécuté sur une station de travail pour développeur locale, il existe des différences de fonctionnalités entre l’émulateur et un compte Azure Cosmos DB dans le cloud :</span><span class="sxs-lookup"><span data-stu-id="beae4-293">Because the Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure Cosmos DB account in the cloud:</span></span>

* <span data-ttu-id="beae4-294">L’émulateur Azure Cosmos DB prend en charge uniquement un compte fixe et une clé principale connue.</span><span class="sxs-lookup"><span data-stu-id="beae4-294">The Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="beae4-295">La régénération de clé n’est pas possible dans l’émulateur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-295">Key regeneration is not possible in the Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="beae4-296">L’émulateur Azure Cosmos DB n’est pas un service de stockage évolutif et ne prend pas en charge un grand nombre de collections.</span><span class="sxs-lookup"><span data-stu-id="beae4-296">The Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="beae4-297">L’émulateur Azure Cosmos DB ne simule pas différents [niveaux de cohérence Azure Cosmos DB](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="beae4-297">The Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="beae4-298">L’émulateur Azure Cosmos DB ne simule pas la [réplication dans plusieurs régions](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="beae4-298">The Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="beae4-299">L’émulateur Azure Cosmos DB ne prend pas en charge les substitutions de quota de service disponibles dans le service Azure Cosmos DB (par exemple, les limites de taille de document ou l’augmentation du stockage d’une collection partitionnée).</span><span class="sxs-lookup"><span data-stu-id="beae4-299">The Azure Cosmos DB Emulator does not support the service quota overrides that are available in the Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="beae4-300">Votre copie de l’émulateur Azure Cosmos DB n’a peut-être pas été mise à jour avec les dernières modifications apportées au service Azure Cosmos DB, donc veuillez consulter la section [Planificateur de capacité Azure Cosmos DB](https://www.documentdb.com/capacityplanner) pour évaluer avec précision les besoins de débit de production (RU) de votre application.</span><span class="sxs-lookup"><span data-stu-id="beae4-300">As your copy of the Azure Cosmos DB Emulator might not be up to date with the most recent changes with the Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="beae4-301"><a id="set-partitioncount"></a>Modification du nombre de collections</span><span class="sxs-lookup"><span data-stu-id="beae4-301"><a id="set-partitioncount"></a>Change the number of collections</span></span>

<span data-ttu-id="beae4-302">À l’aide de l’émulateur Azure Cosmos DB, vous pouvez, par défaut, créer jusqu’à 25 collections à partition unique ou 1 collection partitionnée.</span><span class="sxs-lookup"><span data-stu-id="beae4-302">By default, you can create up to 25 single partition collections, or 1 partitioned collection using the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="beae4-303">En modifiant la valeur **PartitionCount**, vous pouvez créer jusqu'à 250 collections à partition unique ou 10 collections partitionnées, ou n’importe quelle combinaison des deux qui ne dépasse pas 250 partitions uniques (où 1 collection partitionnée = 25 collections à partition unique).</span><span class="sxs-lookup"><span data-stu-id="beae4-303">By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="beae4-304">Si vous tentez de créer une collection après le dépassement du nombre de partitions actuel, l’émulateur lève une exception ServiceUnavailable comportant le message suivant.</span><span class="sxs-lookup"><span data-stu-id="beae4-304">If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="beae4-305">Pour modifier le nombre de collections disponibles dans l’émulateur Azure Cosmos DB, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="beae4-305">To change the number of collections available to the Azure Cosmos DB Emulator, do the following:</span></span>

1. <span data-ttu-id="beae4-306">Supprimez toutes les données locales de l’émulateur Azure Cosmos DB en cliquant avec le bouton droit sur l’icône **Émulateur Azure Cosmos DB** dans la zone d’état, puis en cliquant sur **Reset Data...** (Réinitialiser les données...).</span><span class="sxs-lookup"><span data-stu-id="beae4-306">Delete all local Azure Cosmos DB Emulator data by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="beae4-307">Supprimez toutes les données de l’émulateur dans le dossier C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="beae4-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="beae4-308">Quittez toutes les instances ouvertes en cliquant avec le bouton droit sur l’icône **Émulateur Azure Cosmos DB** dans la zone d’état, puis en cliquant sur **Quitter**.</span><span class="sxs-lookup"><span data-stu-id="beae4-308">Exit all open instances by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="beae4-309">Quitter l’ensemble des instances peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="beae4-309">It may take a minute for all instances to exit.</span></span>
4. <span data-ttu-id="beae4-310">Installez la dernière version de [l’émulateur Azure Cosmos DB](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="beae4-310">Install the latest version of the [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="beae4-311">Lancez l’émulateur avec l’indicateur PartitionCount en définissant une valeur <= 250.</span><span class="sxs-lookup"><span data-stu-id="beae4-311">Launch the emulator with the PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="beae4-312">Par exemple : `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="beae4-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="beae4-313">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="beae4-313">Troubleshooting</span></span>

<span data-ttu-id="beae4-314">Utilisez les conseils suivants pour vous aider à résoudre les problèmes rencontrés avec l’émulateur Azure Cosmos DB :</span><span class="sxs-lookup"><span data-stu-id="beae4-314">Use the following tips to help troubleshoot issues you encounter with the Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="beae4-315">Si vous avez installé une nouvelle version de l’émulateur et si vous rencontrez des erreurs, réinitialisez vos données.</span><span class="sxs-lookup"><span data-stu-id="beae4-315">If you installed a new version of the Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="beae4-316">Pour réinitialiser vos données, cliquez avec le bouton droit sur l’icône de l’émulateur Azure Cosmos DB dans la zone d’état, puis cliquez sur Réinitialiser les données.</span><span class="sxs-lookup"><span data-stu-id="beae4-316">You can reset your data by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="beae4-317">Si cela ne résout pas les erreurs, vous pouvez désinstaller, puis réinstaller l’application.</span><span class="sxs-lookup"><span data-stu-id="beae4-317">If that does not fix the errors, you can uninstall and reinstall the app.</span></span> <span data-ttu-id="beae4-318">Pour obtenir des instructions, consultez [Désinstaller l’émulateur local](#uninstall).</span><span class="sxs-lookup"><span data-stu-id="beae4-318">See [Uninstall the local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="beae4-319">Si l’émulateur Azure Cosmos DB se bloque, collectez les fichiers de vidage dans le dossier sous c:\Utilisateurs\nom_utilisateur\AppData\Local\CrashDumps, compressez-les et joignez-les à un e-mail que vous envoyez à l’adresse [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="beae4-319">If the Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="beae4-320">Si des incidents se produisent dans CosmosDB.StartupEntryPoint.exe, exécutez la commande suivante à partir d’une invite de commandes administrateur : `lodctr /R`.</span><span class="sxs-lookup"><span data-stu-id="beae4-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="beae4-321">Si vous rencontrez un problème de connectivité, [collectez les fichiers de trace](#trace-files), compressez-les et joignez-les à un e-mail à [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="beae4-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="beae4-322">Si vous recevez un message **Service indisponible**, il se peut que l’émulateur n’arrive pas à initialiser la pile réseau.</span><span class="sxs-lookup"><span data-stu-id="beae4-322">If you receive a **Service Unavailable** message, the emulator might be failing to initialize the network stack.</span></span> <span data-ttu-id="beae4-323">Vérifiez si les clients Pulse Secure ou Juniper Networks sont installés, car leurs pilotes de filtre réseau peuvent être à l’origine du problème.</span><span class="sxs-lookup"><span data-stu-id="beae4-323">Check to see if you have the Pulse secure client or Juniper networks client installed, as their network filter drivers may cause the problem.</span></span> <span data-ttu-id="beae4-324">La désinstallation des pilotes de filtre de réseau tiers permet généralement de résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="beae4-324">Uninstalling third party network filter drivers typically fixes the issue.</span></span>

### <span data-ttu-id="beae4-325"><a id="trace-files"></a>Collecter les fichiers de trace</span><span class="sxs-lookup"><span data-stu-id="beae4-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="beae4-326">Pour collecter des traces de débogage, exécutez les commandes suivantes à partir d’une invite de commande d’administration :</span><span class="sxs-lookup"><span data-stu-id="beae4-326">To collect debugging traces, run the following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="beae4-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="beae4-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="beae4-328">Regardez la barre d’état système pour vérifier que le programme s’est arrêté ; l’arrêt peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="beae4-328">Watch the system tray to make sure the program has shut down, it may take a minute.</span></span> <span data-ttu-id="beae4-329">Vous pouvez aussi simplement cliquer sur **Quitter** dans l’interface utilisateur de l’émulateur Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="beae4-329">You can also just click **Exit** in the Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="beae4-330">Reproduisez le problème.</span><span class="sxs-lookup"><span data-stu-id="beae4-330">Reproduce the problem.</span></span> <span data-ttu-id="beae4-331">Si l’Explorateur de données ne fonctionne pas, attendez quelques secondes pour que le navigateur s’ouvre afin d’intercepter l’erreur.</span><span class="sxs-lookup"><span data-stu-id="beae4-331">If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="beae4-332">Accédez à `%ProgramFiles%\Azure Cosmos DB Emulator` et recherchez le fichier docdbemulator_000001.etl.</span><span class="sxs-lookup"><span data-stu-id="beae4-332">Navigate to `%ProgramFiles%\Azure Cosmos DB Emulator` and find the docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="beae4-333">Envoyez le fichier .etl ainsi que les étapes de reproduction à [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="beae4-333">Send the .etl file along with repro steps to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="beae4-334"><a id="uninstall"></a>Désinstaller l’émulateur local</span><span class="sxs-lookup"><span data-stu-id="beae4-334"><a id="uninstall"></a>Uninstall the local Emulator</span></span>

1. <span data-ttu-id="beae4-335">Quittez toutes les instances ouvertes de l’émulateur local en cliquant avec le bouton droit sur l’icône de l’émulateur Azure Cosmos DB dans la zone d’état, puis en cliquant sur Quitter.</span><span class="sxs-lookup"><span data-stu-id="beae4-335">Exit all open instances of the local Emulator by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Exit.</span></span> <span data-ttu-id="beae4-336">Quitter l’ensemble des instances peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="beae4-336">It may take a minute for all instances to exit.</span></span>
2. <span data-ttu-id="beae4-337">Dans la zone de recherche Windows, tapez **Applications et fonctionnalités**, puis cliquez sur le résultat **Applications et fonctionnalités (paramètres système)**.</span><span class="sxs-lookup"><span data-stu-id="beae4-337">In the Windows search box, type **Apps & features** and click on the **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="beae4-338">Dans la liste des applications, faites défiler la page jusqu’à trouver **Émulateur Azure Cosmos DB**, sélectionnez-le, cliquez sur **Désinstaller**, puis confirmez en cliquant de nouveau sur **Désinstaller**.</span><span class="sxs-lookup"><span data-stu-id="beae4-338">In the list of apps, scroll to **Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="beae4-339">Lorsque l’application est désinstallée, accédez au dossier C:\Users\<utilisateur>\AppData\Local\CosmosDBEmulator et supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="beae4-339">When the app is uninstalled, navigate to C:\Users\<user>\AppData\Local\CosmosDBEmulator and delete the folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="beae4-340">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="beae4-340">Next steps</span></span>

<span data-ttu-id="beae4-341">Dans ce didacticiel, vous avez effectué les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="beae4-341">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="beae4-342">Installé l’émulateur local</span><span class="sxs-lookup"><span data-stu-id="beae4-342">Installed the local Emulator</span></span>
> * <span data-ttu-id="beae4-343">Exécuté l’émulateur sur Docker pour Windows</span><span class="sxs-lookup"><span data-stu-id="beae4-343">Rand the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="beae4-344">Authentifié des requêtes</span><span class="sxs-lookup"><span data-stu-id="beae4-344">Authenticated requests</span></span>
> * <span data-ttu-id="beae4-345">Utilisé l’Explorateur de données dans l’émulateur</span><span class="sxs-lookup"><span data-stu-id="beae4-345">Used the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="beae4-346">Exporté des certificats SSL</span><span class="sxs-lookup"><span data-stu-id="beae4-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="beae4-347">Appelé l’émulateur à partir de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="beae4-347">Called the Emulator from the command line</span></span>
> * <span data-ttu-id="beae4-348">Collecté les fichiers de trace</span><span class="sxs-lookup"><span data-stu-id="beae4-348">Collected trace files</span></span>

<span data-ttu-id="beae4-349">Dans ce didacticiel, vous avez appris à utiliser l’émulateur local pour un développement local gratuit.</span><span class="sxs-lookup"><span data-stu-id="beae4-349">In this tutorial, you've learned how to use the local Emulator for free local development.</span></span> <span data-ttu-id="beae4-350">Vous pouvez maintenant passer à l’étape suivante du didacticiel et découvrir comment exporter les certificats SSL de l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="beae4-350">You can now proceed to the next tutorial and learn how to export Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="beae4-351">Exporter les certificats de l’émulateur Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="beae4-351">Export the Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)
