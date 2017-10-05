---
title: Activation de la synchronisation hors connexion pour votre application Azure Mobile App (Cordova) | Microsoft Docs
description: "Découvrez comment utiliser App Service Mobile App pour mettre en cache et synchroniser des données hors connexion dans votre application Cordova"
documentationcenter: cordova
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 1a3f685d-f79d-4f8b-ae11-ff96e79e9de9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-cordova-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 45e80ca672dfdb6defc6e5c1aac3d29f5479125c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="9abc4-103">Activation de la synchronisation hors connexion pour votre application mobile Cordova</span><span class="sxs-lookup"><span data-stu-id="9abc4-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="9abc4-104">Ce didacticiel présente la fonctionnalité de synchronisation hors connexion d’Azure Mobile Apps pour Cordova.</span><span class="sxs-lookup"><span data-stu-id="9abc4-104">This tutorial introduces the offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="9abc4-105">La synchronisation hors connexion permet aux utilisateurs finaux d’interagir avec une application mobile &mdash;pour afficher, ajouter ou modifier des données&mdash;, même lorsqu’il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="9abc4-105">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="9abc4-106">Les modifications sont stockées dans une base de données locale.</span><span class="sxs-lookup"><span data-stu-id="9abc4-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="9abc4-107">Une fois l'appareil de nouveau en ligne, ces modifications sont synchronisées avec le service distant.</span><span class="sxs-lookup"><span data-stu-id="9abc4-107">Once the device is back online, these changes are synced with the remote service.</span></span>

<span data-ttu-id="9abc4-108">Ce didacticiel est basé sur la solution de démarrage rapide de Cordova pour les applications mobiles créées en suivant le didacticiel [Démarrage rapide Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="9abc4-108">This tutorial is based on the Cordova quickstart solution for Mobile Apps that you create when you complete the tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="9abc4-109">Dans ce didacticiel, vous allez mettre à jour la solution de démarrage rapide pour ajouter les fonctionnalités hors connexion d’Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="9abc4-109">In this tutorial, you update the quickstart solution to add offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="9abc4-110">Vous en découvrez également plus sur le code hors connexion spécifique dans l’application.</span><span class="sxs-lookup"><span data-stu-id="9abc4-110">We also highlight the offline-specific code in the app.</span></span>

<span data-ttu-id="9abc4-111">Pour plus d’informations sur la fonctionnalité de synchronisation hors connexion, consultez la rubrique [Synchronisation des données hors connexion dans Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="9abc4-111">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="9abc4-112">Pour plus d’informations d’utilisation de l’API, consultez la [documentation de l’API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="9abc4-112">For details of API usage, see the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-to-the-quickstart-solution"></a><span data-ttu-id="9abc4-113">Ajouter la synchronisation hors connexion à la solution de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="9abc4-113">Add offline sync to the quickstart solution</span></span>
<span data-ttu-id="9abc4-114">Le code de synchronisation hors connexion doit être ajouté à l’application.</span><span class="sxs-lookup"><span data-stu-id="9abc4-114">The offline sync code must be added to the app.</span></span> <span data-ttu-id="9abc4-115">La synchronisation hors connexion requiert le plug-in cordova-sqlite-storage, qui est automatiquement ajouté à votre application lorsque le plug-in Azure Mobile Apps est inclus dans le projet.</span><span class="sxs-lookup"><span data-stu-id="9abc4-115">Offline sync requires the cordova-sqlite-storage plugin, which automatically gets added to your app when the Azure Mobile Apps plugin is included in the project.</span></span> <span data-ttu-id="9abc4-116">Le projet de démarrage rapide inclut ces deux plug-ins.</span><span class="sxs-lookup"><span data-stu-id="9abc4-116">The Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="9abc4-117">Dans l’Explorateur de solutions de Visual Studio, ouvrez le fichier index.js et remplacez le code suivant</span><span class="sxs-lookup"><span data-stu-id="9abc4-117">In Visual Studio's Solution Explorer, open index.js and replace the following code</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable;      // Reference to a table endpoint on backend

    <span data-ttu-id="9abc4-118">par ce code :</span><span class="sxs-lookup"><span data-stu-id="9abc4-118">with this code:</span></span>

        var client,            // Connection to the Azure Mobile App backend
           todoItemTable,      // Reference to a table endpoint on backend
           syncContext;        // Reference to offline data sync context

2. <span data-ttu-id="9abc4-119">Ensuite, remplacez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="9abc4-119">Next, replace the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="9abc4-120">par ce code :</span><span class="sxs-lookup"><span data-stu-id="9abc4-120">with this code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');
        var store = new WindowsAzure.MobileServiceSqliteStore('store.db');

        store.defineTable({
          name: 'todoitem',
          columnDefinitions: {
              id: 'string',
              text: 'string',
              complete: 'boolean',
              version: 'string'
          }
        });

        // Get the sync context from the client
        syncContext = client.getSyncContext();

    <span data-ttu-id="9abc4-121">Les ajouts de code précédents initialisent le magasin local et définissent une table locale correspondant aux valeurs de colonne utilisées dans votre serveur principal Azure.</span><span class="sxs-lookup"><span data-stu-id="9abc4-121">The preceding code additions initialize the local store and define a local table that matches the column values used in your Azure back end.</span></span> <span data-ttu-id="9abc4-122">(Vous n’avez pas besoin d’inclure toutes les valeurs de colonne dans ce code.)  Le champ `version` est géré par le serveur principal mobile et est utilisé pour la résolution des conflits.</span><span class="sxs-lookup"><span data-stu-id="9abc4-122">(You don't need to include all column values in this code.)  The `version` field is maintained by the mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="9abc4-123">Vous obtenez une référence au contexte de synchronisation en appelant **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="9abc4-123">You get a reference to the sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="9abc4-124">Le contexte de synchronisation permet de conserver les relations entre les tables grâce au suivi et à l’envoi des modifications dans toutes les tables qu’une application cliente modifie quand `.push()` est appelé.</span><span class="sxs-lookup"><span data-stu-id="9abc4-124">The sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="9abc4-125">Mettez à jour l’URL de l’application pour l’URL de votre application Mobile App.</span><span class="sxs-lookup"><span data-stu-id="9abc4-125">Update the application URL to your Mobile App application URL.</span></span>

4. <span data-ttu-id="9abc4-126">Ensuite, remplacez ce code :</span><span class="sxs-lookup"><span data-stu-id="9abc4-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is the table name

    <span data-ttu-id="9abc4-127">par ce code :</span><span class="sxs-lookup"><span data-stu-id="9abc4-127">with this code:</span></span>

        // Initialize the sync context with the store
        syncContext.initialize(store).then(function () {

        // Get the local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle the conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert to server's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle the error
                  // In the simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function to perform the actual sync
        syncBackend();

        // Refresh the todoItems
        refreshDisplay();

        // Wire up the UI Event Handler for the Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="9abc4-128">Le code précédent initialise le contexte de synchronisation, puis appelle getSyncTable (au lieu de getTable) pour obtenir une référence à la table locale.</span><span class="sxs-lookup"><span data-stu-id="9abc4-128">The preceding code initializes the sync context and then calls getSyncTable (instead of getTable) to get a reference to the local table.</span></span>

    <span data-ttu-id="9abc4-129">Ce code utilise la base de données locale pour toutes les opérations de table CRUD (Create, Read, Update et Delete - Créer, Lire, Mettre à jour et Supprimer).</span><span class="sxs-lookup"><span data-stu-id="9abc4-129">This code uses the local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="9abc4-130">Cet exemple effectue une simple gestion des erreurs sur les conflits de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="9abc4-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="9abc4-131">Une application réelle gèrerait les différentes erreurs telles que les conditions du réseau, les conflits de serveur et autres.</span><span class="sxs-lookup"><span data-stu-id="9abc4-131">A real application would handle the various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="9abc4-132">Pour plus d’exemples de code, consultez l’ [l’exemple de synchronisation hors connexion].</span><span class="sxs-lookup"><span data-stu-id="9abc4-132">For code examples, see the [offline sync sample].</span></span>

5. <span data-ttu-id="9abc4-133">Ensuite, ajoutez cette fonction pour effectuer la synchronisation réelle.</span><span class="sxs-lookup"><span data-stu-id="9abc4-133">Next, add this function to perform the actual sync.</span></span>

        function syncBackend() {

          // Sync local store to Azure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from the Azure table after syncing to Azure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="9abc4-134">Vous décidez du moment auquel envoyer les modifications au serveur principal Mobile App en appelant **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="9abc4-134">You decide when to push changes to the Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="9abc4-135">Par exemple, vous pouvez appeler **syncBackend** dans un gestionnaire d’événement de bouton lié à un bouton de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="9abc4-135">For example, you could call **syncBackend** in a button event handler tied to a sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="9abc4-136">Considérations relatives à la synchronisation hors connexion</span><span class="sxs-lookup"><span data-stu-id="9abc4-136">Offline sync considerations</span></span>

<span data-ttu-id="9abc4-137">Dans l’exemple, la méthode **push** de **syncContext** n’est appelée qu’au démarrage de l’application dans la fonction de rappel pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="9abc4-137">In the sample, the **push** method of **syncContext** is only called on app startup in the callback function for login.</span></span>  <span data-ttu-id="9abc4-138">Dans une application réelle, vous pourriez également provoquer manuellement le déclenchement de la fonctionnalité de synchronisation lorsque l’état du réseau change.</span><span class="sxs-lookup"><span data-stu-id="9abc4-138">In a real-world application, you could also make this sync functionality triggered manually or when the network state changes.</span></span>

<span data-ttu-id="9abc4-139">Si une extraction est exécutée sur une table qui comporte des mises à jour locales en attente faisant l’objet d’un suivi en fonction du contexte, cette opération déclenche automatiquement un envoi.</span><span class="sxs-lookup"><span data-stu-id="9abc4-139">When a pull is executed against a table that has pending local updates tracked by the context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="9abc4-140">Lors de l’actualisation, de l’ajout et de l’achèvement des éléments dans cet exemple, vous pouvez omettre l’appel explicite de **push**, puisqu’il peut être redondant.</span><span class="sxs-lookup"><span data-stu-id="9abc4-140">When refreshing, adding, and completing items in this sample, you can omit the explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="9abc4-141">Dans le code fourni, tous les enregistrements de la table TodoItem distante sont interrogés, mais il est également possible de filtrer les enregistrements en transmettant un ID de requête et une requête à **push**.</span><span class="sxs-lookup"><span data-stu-id="9abc4-141">In the provided code, all records in the remote todoItem table are queried, but it is also possible to filter records by passing a query id and query to **push**.</span></span> <span data-ttu-id="9abc4-142">Pour plus d’informations, consultez la section *Synchronisation incrémentielle* dans [Synchronisation des données hors connexion dans Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="9abc4-142">For more information, see the section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="9abc4-143">(Facultatif) Désactiver l’authentification</span><span class="sxs-lookup"><span data-stu-id="9abc4-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="9abc4-144">Si vous ne souhaitez pas le faire avant de tester la synchronisation hors connexion, commentez la fonction de rappel pour la connexion, mais pas le code à l’intérieur de la fonction de rappel.</span><span class="sxs-lookup"><span data-stu-id="9abc4-144">If you don't want to set up authentication before testing offline sync, comment out the callback function for login, but leave the code inside the callback function uncommented.</span></span>  <span data-ttu-id="9abc4-145">Après avoir commenté les lignes de connexion, le code suit :</span><span class="sxs-lookup"><span data-stu-id="9abc4-145">After commenting out the login lines, the code follows:</span></span>

      // Login to the service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave the rest of the code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="9abc4-146">À présent, l’application se synchronise avec le serveur principal Azure lorsque vous exécutez l’application.</span><span class="sxs-lookup"><span data-stu-id="9abc4-146">Now, the app syncs with the Azure backend when you run the app.</span></span>

## <a name="run-the-client-app"></a><span data-ttu-id="9abc4-147">Exécuter l’application cliente</span><span class="sxs-lookup"><span data-stu-id="9abc4-147">Run the client app</span></span>
<span data-ttu-id="9abc4-148">Maintenant que la synchronisation hors connexion est activée, vous pouvez exécuter l’application cliente au moins une fois sur chaque plateforme pour remplir la base de données du magasin local.</span><span class="sxs-lookup"><span data-stu-id="9abc4-148">With offline sync now enabled, you can run the client application at least once on each platform to populate the local store database.</span></span> <span data-ttu-id="9abc4-149">Ensuite, simulez un scénario hors connexion et modifiez les données du magasin local pendant que l’application est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="9abc4-149">Later, simulate an offline scenario and modify the data in the local store while the app is offline.</span></span>

## <a name="optional-test-the-sync-behavior"></a><span data-ttu-id="9abc4-150">(Facultatif) Tester le comportement de synchronisation</span><span class="sxs-lookup"><span data-stu-id="9abc4-150">(Optional) Test the sync behavior</span></span>
<span data-ttu-id="9abc4-151">Dans cette section, vous modifiez le projet client pour simuler un scénario hors connexion à l’aide d’une URL d’application non valide pour votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="9abc4-151">In this section, you modify the client project to simulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="9abc4-152">Quand vous ajoutez ou modifiez des éléments de données, ces modifications sont conservées dans le magasin local, mais ne sont synchronisées avec le magasin de données principal qu’une fois la connexion rétablie.</span><span class="sxs-lookup"><span data-stu-id="9abc4-152">When you add or change data items, these changes are held in the local store, but are not synced to the backend data store until the connection is re-established.</span></span>

1. <span data-ttu-id="9abc4-153">Dans l’Explorateur de solutions, ouvrez le fichier de projet index.js et changez l’URL de l’application pour pointer vers une URL non valide, comme dans le code suivant :</span><span class="sxs-lookup"><span data-stu-id="9abc4-153">In the Solution Explorer, open the index.js project file and change the application URL to point to  an invalid URL, like the following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="9abc4-154">Dans index.html, mettez à jour l’élément CSP `<meta>` avec la même URL non valide.</span><span class="sxs-lookup"><span data-stu-id="9abc4-154">In index.html, update the CSP `<meta>` element with the same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="9abc4-155">Créez et exécutez l’application cliente et notez qu’une exception est consignée dans la console lorsque l’application tente de se synchroniser avec le backend après la connexion.</span><span class="sxs-lookup"><span data-stu-id="9abc4-155">Build and run the client app and notice that an exception is logged in the console when the app attempts to sync with the backend after login.</span></span> <span data-ttu-id="9abc4-156">Les nouveaux éléments que vous ajoutez se trouvent uniquement dans le magasin local jusqu’à ce qu’ils puissent être transmis par push vers le serveur principal mobile.</span><span class="sxs-lookup"><span data-stu-id="9abc4-156">Any new items you add exist only in the local store until they are pushed to the mobile backend.</span></span> <span data-ttu-id="9abc4-157">L’application cliente se comporte comme si elle était connectée au serveur principal.</span><span class="sxs-lookup"><span data-stu-id="9abc4-157">The client app behaves as if it is connected to the backend.</span></span>

4. <span data-ttu-id="9abc4-158">Fermez l’application et redémarrez-la pour vérifier que les nouveaux élément que vous avez créés sont conservés dans le magasin local.</span><span class="sxs-lookup"><span data-stu-id="9abc4-158">Close the app and restart it to verify that the new items you created are persisted to the local store.</span></span>

5. <span data-ttu-id="9abc4-159">(Facultatif) À l’aide de Visual Studio, affichez votre table Azure SQL Database pour constater que les données dans la base de données backend n’ont pas changé.</span><span class="sxs-lookup"><span data-stu-id="9abc4-159">(Optional) Use Visual Studio to view your Azure SQL Database table to see that the data in the backend database has not changed.</span></span>

    <span data-ttu-id="9abc4-160">Dans Visual Studio, ouvrez l' **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="9abc4-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="9abc4-161">Accédez à votre base de données dans **Azure**->**Bases de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="9abc4-161">Navigate to your database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="9abc4-162">Cliquez avec le bouton droit sur votre base de données, puis sélectionnez **Ouvrir dans l’Explorateur d’objets SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="9abc4-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="9abc4-163">Maintenant, vous pouvez accéder à votre table de base de données SQL et à son contenu.</span><span class="sxs-lookup"><span data-stu-id="9abc4-163">Now you can browse to your SQL database table and its contents.</span></span>

## <a name="optional-test-the-reconnection-to-your-mobile-backend"></a><span data-ttu-id="9abc4-164">(Facultatif) Tester la reconnexion à votre backend</span><span class="sxs-lookup"><span data-stu-id="9abc4-164">(Optional) Test the reconnection to your mobile backend</span></span>

<span data-ttu-id="9abc4-165">Dans cette section, vous reconnectez l'application au serveur principal mobile, ce qui simule le retour de l'application à un état en ligne.</span><span class="sxs-lookup"><span data-stu-id="9abc4-165">In this section, you reconnect the app to the mobile backend, which simulates the app coming back to an online state.</span></span> <span data-ttu-id="9abc4-166">Lorsque vous vous connectez, les données sont synchronisées avec votre serveur principal mobile.</span><span class="sxs-lookup"><span data-stu-id="9abc4-166">When you log in, data is synced to your mobile backend.</span></span>

1. <span data-ttu-id="9abc4-167">Rouvrez index.js et restaurez l’URL de l’application.</span><span class="sxs-lookup"><span data-stu-id="9abc4-167">Reopen index.js and restore the application URL.</span></span>
2. <span data-ttu-id="9abc4-168">Rouvrez le fichier index.html et corrigez l’URL de l’application dans l’élément CSP `<meta>` .</span><span class="sxs-lookup"><span data-stu-id="9abc4-168">Reopen index.html and correct the application URL in the CSP `<meta>` element.</span></span>
3. <span data-ttu-id="9abc4-169">Régénérez et exécutez l’application cliente.</span><span class="sxs-lookup"><span data-stu-id="9abc4-169">Rebuild and run the client app.</span></span> <span data-ttu-id="9abc4-170">Après la connexion, l’application tente de se synchroniser avec le backend Mobile App.</span><span class="sxs-lookup"><span data-stu-id="9abc4-170">The app attempts to sync with the mobile app backend after login.</span></span> <span data-ttu-id="9abc4-171">Vérifiez qu’aucune exception n’est consignée dans la console de débogage.</span><span class="sxs-lookup"><span data-stu-id="9abc4-171">Verify that no exceptions are logged in the debug console.</span></span>
4. <span data-ttu-id="9abc4-172">(Facultatif) Affichez les données mises à jour à l’aide de l’Explorateur d’objets SQL Server ou d’un outil REST tel que Fiddler.</span><span class="sxs-lookup"><span data-stu-id="9abc4-172">(Optional) View the updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="9abc4-173">Notez que les données n’ont pas été synchronisées entre la base de données du serveur principal et le magasin local.</span><span class="sxs-lookup"><span data-stu-id="9abc4-173">Notice the data has been synchronized between the backend database and the local store.</span></span>

    <span data-ttu-id="9abc4-174">Notez que les données ont été synchronisées entre la base de données et le magasin local et qu’elles contiennent les éléments que vous avez ajoutés pendant que votre application était déconnectée.</span><span class="sxs-lookup"><span data-stu-id="9abc4-174">Notice the data has been synchronized between the database and the local store and contains the items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9abc4-175">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="9abc4-175">Additional resources</span></span>
* <span data-ttu-id="9abc4-176">[Synchronisation des données hors connexion dans Azure Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="9abc4-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="9abc4-177">[Visual Studio Tools pour Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="9abc4-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="9abc4-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9abc4-178">Next steps</span></span>
* <span data-ttu-id="9abc4-179">Consultez les fonctionnalités de synchronisation hors connexion plus avancées, comme la résolution des conflits dans [l’exemple de synchronisation hors connexion]</span><span class="sxs-lookup"><span data-stu-id="9abc4-179">Review more advanced offline sync features such as conflict resolution in the [offline sync sample]</span></span>
* <span data-ttu-id="9abc4-180">Consultez la référence de l’API de synchronisation hors connexion dans la [documentation de l’API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="9abc4-180">Review the offline sync API reference in the [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
<span data-ttu-id="9abc4-181">[Démarrage rapide Apache Cordova]: app-service-mobile-cordova-get-started.md</span><span class="sxs-lookup"><span data-stu-id="9abc4-181">[Apache Cordova quick start]: app-service-mobile-cordova-get-started.md</span></span>
<span data-ttu-id="9abc4-182">[l’exemple de synchronisation hors connexion]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span><span class="sxs-lookup"><span data-stu-id="9abc4-182">[offline sync sample]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling</span></span>
<span data-ttu-id="9abc4-183">[Synchronisation des données hors connexion dans Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="9abc4-183">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with the .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
<span data-ttu-id="9abc4-184">[Visual Studio Tools pour Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span><span class="sxs-lookup"><span data-stu-id="9abc4-184">[Visual Studio Tools for Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx</span></span>
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
