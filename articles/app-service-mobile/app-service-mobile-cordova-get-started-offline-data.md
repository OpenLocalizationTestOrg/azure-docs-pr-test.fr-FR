---
title: aaaEnable la synchronisation hors connexion pour votre application Mobile de Azure (Cordova) | Documents Microsoft
description: "Découvrez comment toouse l’application Mobile App Service toocache et la synchronisation de données hors connexion dans votre application Cordova"
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
ms.openlocfilehash: 4e6ae96c3d96dac8ebb3749354b83a04686831b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-cordova-mobile-app"></a><span data-ttu-id="a292d-103">Activation de la synchronisation hors connexion pour votre application mobile Cordova</span><span class="sxs-lookup"><span data-stu-id="a292d-103">Enable offline sync for your Cordova mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

<span data-ttu-id="a292d-104">Ce didacticiel présente la fonctionnalité de synchronisation hors connexion hello des applications mobiles Azure pour Cordova.</span><span class="sxs-lookup"><span data-stu-id="a292d-104">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Cordova.</span></span> <span data-ttu-id="a292d-105">Synchronisation hors connexion permet toointeract des utilisateurs finaux avec une application mobile&mdash;affichage, l’ajout ou la modification des données&mdash;même quand il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="a292d-105">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="a292d-106">Les modifications sont stockées dans une base de données locale.</span><span class="sxs-lookup"><span data-stu-id="a292d-106">Changes are stored in a local database.</span></span>  <span data-ttu-id="a292d-107">Une fois que l’appareil de hello est remis en ligne, ces modifications sont synchronisées avec le service distant hello.</span><span class="sxs-lookup"><span data-stu-id="a292d-107">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="a292d-108">Ce didacticiel est basé sur hello solution de démarrage rapide de Cordova pour des applications mobiles que vous créez lorsque vous terminez hello didacticiel [démarrage rapide d’Apache Cordova].</span><span class="sxs-lookup"><span data-stu-id="a292d-108">This tutorial is based on hello Cordova quickstart solution for Mobile Apps that you create when you complete hello tutorial [Apache Cordova quick start].</span></span> <span data-ttu-id="a292d-109">Dans ce didacticiel, vous mettez à jour hello quickstart solution tooadd des fonctions hors connexion des applications mobiles Azure.</span><span class="sxs-lookup"><span data-stu-id="a292d-109">In this tutorial, you update hello quickstart solution tooadd offline features of Azure Mobile Apps.</span></span>  <span data-ttu-id="a292d-110">Nous avons également en surbrillance code hors connexion spécifiques de hello dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a292d-110">We also highlight hello offline-specific code in hello app.</span></span>

<span data-ttu-id="a292d-111">toolearn en savoir plus sur la fonctionnalité de synchronisation hors connexion hello, consultez rubrique de hello [synchronisation des données hors connexion dans les applications mobiles Azure].</span><span class="sxs-lookup"><span data-stu-id="a292d-111">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span> <span data-ttu-id="a292d-112">Pour plus d’informations d’utilisation de l’API, consultez hello [documentation de l’API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="a292d-112">For details of API usage, see hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

## <a name="add-offline-sync-toohello-quickstart-solution"></a><span data-ttu-id="a292d-113">Ajouter la solution de démarrage rapide de toohello de synchronisation hors connexion</span><span class="sxs-lookup"><span data-stu-id="a292d-113">Add offline sync toohello quickstart solution</span></span>
<span data-ttu-id="a292d-114">code de synchronisation hors connexion Hello doit être ajouté toohello application.</span><span class="sxs-lookup"><span data-stu-id="a292d-114">hello offline sync code must be added toohello app.</span></span> <span data-ttu-id="a292d-115">Synchronisation hors connexion requiert un plug-in cordova-sqlite-stockage hello qui est automatiquement ajouté tooyour application lorsque le plug-in des applications mobiles Azure hello est inclus dans le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="a292d-115">Offline sync requires hello cordova-sqlite-storage plugin, which automatically gets added tooyour app when hello Azure Mobile Apps plugin is included in hello project.</span></span> <span data-ttu-id="a292d-116">projet de démarrage rapide de Hello inclut les deux de ces plug-ins.</span><span class="sxs-lookup"><span data-stu-id="a292d-116">hello Quickstart project includes both of these plugins.</span></span>

1. <span data-ttu-id="a292d-117">Dans l’Explorateur de solutions de Visual Studio, ouvrez index.js et remplacez hello suivant de code</span><span class="sxs-lookup"><span data-stu-id="a292d-117">In Visual Studio's Solution Explorer, open index.js and replace hello following code</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable;      // Reference tooa table endpoint on backend

    <span data-ttu-id="a292d-118">par ce code :</span><span class="sxs-lookup"><span data-stu-id="a292d-118">with this code:</span></span>

        var client,            // Connection toohello Azure Mobile App backend
           todoItemTable,      // Reference tooa table endpoint on backend
           syncContext;        // Reference toooffline data sync context

2. <span data-ttu-id="a292d-119">Ensuite, remplacez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="a292d-119">Next, replace hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net');

    <span data-ttu-id="a292d-120">par ce code :</span><span class="sxs-lookup"><span data-stu-id="a292d-120">with this code:</span></span>

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

        // Get hello sync context from hello client
        syncContext = client.getSyncContext();

    <span data-ttu-id="a292d-121">initialiser le magasin local de hello Hello ajouts de code précédent et définir une table locale qui correspond aux valeurs de colonne hello utilisés dans votre Azure back-end.</span><span class="sxs-lookup"><span data-stu-id="a292d-121">hello preceding code additions initialize hello local store and define a local table that matches hello column values used in your Azure back end.</span></span> <span data-ttu-id="a292d-122">(Vous n’avez pas besoin tooinclude toutes les valeurs de colonne dans ce code.)  Hello `version` champ est géré par le service principal mobile de hello et est utilisé pour la résolution de conflit.</span><span class="sxs-lookup"><span data-stu-id="a292d-122">(You don't need tooinclude all column values in this code.)  hello `version` field is maintained by hello mobile backend and is used for conflict resolution.</span></span>

    <span data-ttu-id="a292d-123">Vous obtenez un contexte de synchronisation toohello référence en appelant **getSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="a292d-123">You get a reference toohello sync context by calling **getSyncContext**.</span></span> <span data-ttu-id="a292d-124">Hello contexte de synchronisation permet de conserver les relations entre les tables en effectuant le suivi en exécutant un push des modifications dans toutes les tables, une application cliente a modifié lorsque `.push()` est appelée.</span><span class="sxs-lookup"><span data-stu-id="a292d-124">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when `.push()` is called.</span></span>

3. <span data-ttu-id="a292d-125">Mettre à jour des URL de l’application hello application URL tooyour l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="a292d-125">Update hello application URL tooyour Mobile App application URL.</span></span>

4. <span data-ttu-id="a292d-126">Ensuite, remplacez ce code :</span><span class="sxs-lookup"><span data-stu-id="a292d-126">Next, replace this code:</span></span>

        todoItemTable = client.getTable('todoitem'); // todoitem is hello table name

    <span data-ttu-id="a292d-127">par ce code :</span><span class="sxs-lookup"><span data-stu-id="a292d-127">with this code:</span></span>

        // Initialize hello sync context with hello store
        syncContext.initialize(store).then(function () {

        // Get hello local table reference.
        todoItemTable = client.getSyncTable('todoitem');

        syncContext.pushHandler = {
            onConflict: function (pushError) {
                // Handle hello conflict.
                console.log("Sync conflict! " + pushError.getError().message);
                // Update failed, revert tooserver's copy.
                pushError.cancelAndDiscard();
              },
              onError: function (pushError) {
                  // Handle hello error
                  // In hello simulated offline state, you get "Sync error! Unexpected connection failure."
                  console.log("Sync error! " + pushError.getError().message);
              }
        };

        // Call a function tooperform hello actual sync
        syncBackend();

        // Refresh hello todoItems
        refreshDisplay();

        // Wire up hello UI Event Handler for hello Add Item
        $('#add-item').submit(addItemHandler);
        $('#refresh').on('click', refreshDisplay);

    <span data-ttu-id="a292d-128">Hello précédent code initialise le contexte de synchronisation hello, puis appelle getSyncTable (au lieu de getTable) tooget une table locale toohello de référence.</span><span class="sxs-lookup"><span data-stu-id="a292d-128">hello preceding code initializes hello sync context and then calls getSyncTable (instead of getTable) tooget a reference toohello local table.</span></span>

    <span data-ttu-id="a292d-129">Ce code utilise hello base de données locale pour tous les créer, lire, mettre à jour et supprimer (CRUD) des opérations de table.</span><span class="sxs-lookup"><span data-stu-id="a292d-129">This code uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span>

    <span data-ttu-id="a292d-130">Cet exemple effectue une simple gestion des erreurs sur les conflits de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="a292d-130">This sample performs simple error handling on sync conflicts.</span></span> <span data-ttu-id="a292d-131">Une application réelle traiterait hello diverses erreurs telles que les conditions du réseau, le serveur est en conflit et d’autres.</span><span class="sxs-lookup"><span data-stu-id="a292d-131">A real application would handle hello various errors like network conditions, server conflicts, and others.</span></span> <span data-ttu-id="a292d-132">Pour des exemples de code, consultez hello [exemple de synchronisation hors connexion].</span><span class="sxs-lookup"><span data-stu-id="a292d-132">For code examples, see hello [offline sync sample].</span></span>

5. <span data-ttu-id="a292d-133">Ensuite, ajoutez cette synchronisation réels de fonction tooperform hello.</span><span class="sxs-lookup"><span data-stu-id="a292d-133">Next, add this function tooperform hello actual sync.</span></span>

        function syncBackend() {

          // Sync local store tooAzure table when app loads, or when login complete.
          syncContext.push().then(function () {
              // Push completed

          });

          // Pull items from hello Azure table after syncing tooAzure.
          syncContext.pull(new WindowsAzure.Query('todoitem'));
        }

    <span data-ttu-id="a292d-134">Vous décidez lorsque toopush devient le principal de l’application Mobile toohello en appelant **syncContext.push()**.</span><span class="sxs-lookup"><span data-stu-id="a292d-134">You decide when toopush changes toohello Mobile App backend by calling **syncContext.push()**.</span></span> <span data-ttu-id="a292d-135">Par exemple, vous pouvez appeler **syncBackend** dans un bouton synchronisation tooa liée du Gestionnaire d’événements bouton.</span><span class="sxs-lookup"><span data-stu-id="a292d-135">For example, you could call **syncBackend** in a button event handler tied tooa sync button.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="a292d-136">Considérations relatives à la synchronisation hors connexion</span><span class="sxs-lookup"><span data-stu-id="a292d-136">Offline sync considerations</span></span>

<span data-ttu-id="a292d-137">Dans l’exemple hello, hello **push** méthode **syncContext** est appelée uniquement sur le démarrage de l’application dans la fonction de rappel hello pour la connexion.</span><span class="sxs-lookup"><span data-stu-id="a292d-137">In hello sample, hello **push** method of **syncContext** is only called on app startup in hello callback function for login.</span></span>  <span data-ttu-id="a292d-138">Dans une application réelle, vous pouvez également apporter cette fonctionnalité de synchronisation déclenchée manuellement ou que hello réseau état change.</span><span class="sxs-lookup"><span data-stu-id="a292d-138">In a real-world application, you could also make this sync functionality triggered manually or when hello network state changes.</span></span>

<span data-ttu-id="a292d-139">Lorsqu’une extraction est exécutée sur une table qui comporte en attente mises à jour locales suivies par le contexte de hello, qui extrait les opération automatiquement les déclencheurs de push.</span><span class="sxs-lookup"><span data-stu-id="a292d-139">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a push.</span></span> <span data-ttu-id="a292d-140">Lors de l’actualisation, l’ajout et la fin des éléments dans cet exemple, vous pouvez omettre hello explicite **push** appeler, dans la mesure où il peut être redondant.</span><span class="sxs-lookup"><span data-stu-id="a292d-140">When refreshing, adding, and completing items in this sample, you can omit hello explicit **push** call, since it may be redundant.</span></span>

<span data-ttu-id="a292d-141">Dans le code hello fourni, tous les enregistrements dans la table todoItem à distance de hello sont interrogées, mais il est également possible de toofilter enregistrements en passant un id de requête et une requête trop**push**.</span><span class="sxs-lookup"><span data-stu-id="a292d-141">In hello provided code, all records in hello remote todoItem table are queried, but it is also possible toofilter records by passing a query id and query too**push**.</span></span> <span data-ttu-id="a292d-142">Pour plus d’informations, consultez la section de hello *synchronisation incrémentielle* dans [synchronisation des données hors connexion dans les applications mobiles Azure].</span><span class="sxs-lookup"><span data-stu-id="a292d-142">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="optional-disable-authentication"></a><span data-ttu-id="a292d-143">(Facultatif) Désactiver l’authentification</span><span class="sxs-lookup"><span data-stu-id="a292d-143">(Optional) Disable authentication</span></span>

<span data-ttu-id="a292d-144">Si vous ne souhaitez tooset une authentification avant de tester la synchronisation hors connexion, commentez la fonction de rappel hello pour la connexion, mais laissez code hello à l’intérieur de la fonction de rappel hello pas commentée.</span><span class="sxs-lookup"><span data-stu-id="a292d-144">If you don't want tooset up authentication before testing offline sync, comment out hello callback function for login, but leave hello code inside hello callback function uncommented.</span></span>  <span data-ttu-id="a292d-145">Après avoir commenté de lignes de connexion hello, code de hello suit :</span><span class="sxs-lookup"><span data-stu-id="a292d-145">After commenting out hello login lines, hello code follows:</span></span>

      // Login toohello service.
      // client.login('twitter')
      //    .then(function () {
        syncContext.initialize(store).then(function () {
          // Leave hello rest of hello code in this callback function  uncommented.
                ...
        });
      // }, handleError);

<span data-ttu-id="a292d-146">Maintenant, hello application se synchronise avec hello Azure principal lorsque vous exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a292d-146">Now, hello app syncs with hello Azure backend when you run hello app.</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="a292d-147">Exécuter l’application cliente de hello</span><span class="sxs-lookup"><span data-stu-id="a292d-147">Run hello client app</span></span>
<span data-ttu-id="a292d-148">La synchronisation hors connexion est maintenant activée, vous pouvez exécuter application cliente de hello au moins une fois sur chaque plateforme pour remplir la base de données du magasin local hello.</span><span class="sxs-lookup"><span data-stu-id="a292d-148">With offline sync now enabled, you can run hello client application at least once on each platform to populate hello local store database.</span></span> <span data-ttu-id="a292d-149">Une version ultérieure, de simuler un scénario hors connexion et de modifier des données de hello dans le magasin local de hello lors de l’application hello est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="a292d-149">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="optional-test-hello-sync-behavior"></a><span data-ttu-id="a292d-150">(Facultatif) Tester le comportement de synchronisation hello</span><span class="sxs-lookup"><span data-stu-id="a292d-150">(Optional) Test hello sync behavior</span></span>
<span data-ttu-id="a292d-151">Dans cette section, vous modifiez hello client projet toosimulate un scénario hors connexion à l’aide d’une URL d’application non valide pour votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="a292d-151">In this section, you modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="a292d-152">Lorsque vous ajoutez ou modifiez des éléments de données, ces modifications sont conservées dans le magasin local, mais ne sont pas synchronisés toohello magasin de données principal jusqu'à ce que la connexion de hello est rétablie.</span><span class="sxs-lookup"><span data-stu-id="a292d-152">When you add or change data items, these changes are held in the local store, but are not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="a292d-153">Dans l’Explorateur de solutions de hello, ouvrir le fichier de projet index.js hello et modifiez les hello application URL toopoint vers une URL non valide, comme hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="a292d-153">In hello Solution Explorer, open hello index.js project file and change hello application URL toopoint to  an invalid URL, like hello following code:</span></span>

        client = new WindowsAzure.MobileServiceClient('http://yourmobileapp.azurewebsites.net-fail');

2. <span data-ttu-id="a292d-154">Dans index.html, mettre à jour de hello CSP `<meta>` élément avec hello même URL non valide.</span><span class="sxs-lookup"><span data-stu-id="a292d-154">In index.html, update hello CSP `<meta>` element with hello same invalid URL.</span></span>

        <meta http-equiv="Content-Security-Policy" content="default-src 'self' data: gap: http://yourmobileapp.azurewebsites.net-fail; style-src 'self'; media-src *">

3. <span data-ttu-id="a292d-155">Générer et exécuter l’application cliente de hello et notez qu’une exception est enregistrée dans la console hello lors de l’application hello tente de se synchroniser avec le serveur principal hello après la connexion.</span><span class="sxs-lookup"><span data-stu-id="a292d-155">Build and run hello client app and notice that an exception is logged in hello console when hello app attempts to sync with hello backend after login.</span></span> <span data-ttu-id="a292d-156">Les nouveaux éléments que vous ajoutez existent uniquement dans le magasin local de hello jusqu'à ce qu’elles sont appliquées backend mobile de toohello.</span><span class="sxs-lookup"><span data-stu-id="a292d-156">Any new items you add exist only in hello local store until they are pushed toohello mobile backend.</span></span> <span data-ttu-id="a292d-157">Hello client application se comporte comme si elle était connectée toohello principal.</span><span class="sxs-lookup"><span data-stu-id="a292d-157">hello client app behaves as if it is connected toohello backend.</span></span>

4. <span data-ttu-id="a292d-158">Fermez l’application hello et redémarrez-le tooverify que hello nouveaux éléments que vous avez créé sont magasin local de toohello persistante.</span><span class="sxs-lookup"><span data-stu-id="a292d-158">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>

5. <span data-ttu-id="a292d-159">(Facultatif) Utilisez Visual Studio tooview votre toosee de table de base de données SQL Azure données hello dans la base de données principale hello n’a pas changé.</span><span class="sxs-lookup"><span data-stu-id="a292d-159">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="a292d-160">Dans Visual Studio, ouvrez l' **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="a292d-160">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="a292d-161">Accédez de la base de données tooyour dans **Azure**->**bases de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="a292d-161">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="a292d-162">Cliquez avec le bouton droit sur votre base de données, puis sélectionnez **Ouvrir dans l’Explorateur d’objets SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="a292d-162">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="a292d-163">Vous pouvez maintenant rechercher table de base de données SQL tooyour et son contenu.</span><span class="sxs-lookup"><span data-stu-id="a292d-163">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="optional-test-hello-reconnection-tooyour-mobile-backend"></a><span data-ttu-id="a292d-164">(Facultatif) Test hello reconnexion tooyour backend mobile</span><span class="sxs-lookup"><span data-stu-id="a292d-164">(Optional) Test hello reconnection tooyour mobile backend</span></span>

<span data-ttu-id="a292d-165">Dans cette section, vous reconnecter hello toohello mobile serveur principal d’application, ce qui simule l’application hello revenir à un état en ligne.</span><span class="sxs-lookup"><span data-stu-id="a292d-165">In this section, you reconnect hello app toohello mobile backend, which simulates hello app coming back to an online state.</span></span> <span data-ttu-id="a292d-166">Lors de la connexion, les données sont synchronisés tooyour les backend mobile.</span><span class="sxs-lookup"><span data-stu-id="a292d-166">When you log in, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="a292d-167">Rouvrez index.js et de restauration des URL de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="a292d-167">Reopen index.js and restore hello application URL.</span></span>
2. <span data-ttu-id="a292d-168">Rouvrez index.html et corriger les URL de l’application hello Bonjour CSP `<meta>` élément.</span><span class="sxs-lookup"><span data-stu-id="a292d-168">Reopen index.html and correct hello application URL in hello CSP `<meta>` element.</span></span>
3. <span data-ttu-id="a292d-169">Regénérez et exécutez l’application cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="a292d-169">Rebuild and run hello client app.</span></span> <span data-ttu-id="a292d-170">application Hello tentatives toosync avec le serveur principal d’application mobile hello après la connexion.</span><span class="sxs-lookup"><span data-stu-id="a292d-170">hello app attempts toosync with hello mobile app backend after login.</span></span> <span data-ttu-id="a292d-171">Vérifiez qu’aucune exceptions ne sont enregistrées dans la console de débogage hello.</span><span class="sxs-lookup"><span data-stu-id="a292d-171">Verify that no exceptions are logged in hello debug console.</span></span>
4. <span data-ttu-id="a292d-172">(Facultatif) Hello d’affichage mis à jour les données à l’aide de l’Explorateur d’objets SQL Server ou d’un outil REST, comme Fiddler.</span><span class="sxs-lookup"><span data-stu-id="a292d-172">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler.</span></span> <span data-ttu-id="a292d-173">Les données de salutation avis a été synchronisées entre la base de données principale hello et magasin local de hello.</span><span class="sxs-lookup"><span data-stu-id="a292d-173">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="a292d-174">Notez que les données de salutation a été synchronisées entre la base de données hello et magasin local de hello et contient les éléments hello que vous avez ajouté pendant que votre application a été déconnectée.</span><span class="sxs-lookup"><span data-stu-id="a292d-174">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a292d-175">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a292d-175">Additional resources</span></span>
* <span data-ttu-id="a292d-176">[synchronisation des données hors connexion dans les applications mobiles Azure]</span><span class="sxs-lookup"><span data-stu-id="a292d-176">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="a292d-177">[Visual Studio Tools pour Apache Cordova]</span><span class="sxs-lookup"><span data-stu-id="a292d-177">[Visual Studio Tools for Apache Cordova]</span></span>

## <a name="next-steps"></a><span data-ttu-id="a292d-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a292d-178">Next steps</span></span>
* <span data-ttu-id="a292d-179">Vérification des fonctionnalités de synchronisation hors connexion tels que la résolution de conflit Bonjour avancées supplémentaires [exemple de synchronisation hors connexion]</span><span class="sxs-lookup"><span data-stu-id="a292d-179">Review more advanced offline sync features such as conflict resolution in hello [offline sync sample]</span></span>
* <span data-ttu-id="a292d-180">Passez en revue la synchronisation hors connexion hello référence d’API Bonjour [documentation de l’API](https://azure.github.io/azure-mobile-apps-js-client).</span><span class="sxs-lookup"><span data-stu-id="a292d-180">Review hello offline sync API reference in hello [API documentation](https://azure.github.io/azure-mobile-apps-js-client).</span></span>

<!-- ##Summary -->

<!-- Images -->

<!-- URLs. -->
[démarrage rapide d’Apache Cordova]: app-service-mobile-cordova-get-started.md
[exemple de synchronisation hors connexion]: https://github.com/Azure-Samples/app-service-mobile-cordova-client-conflict-handling
[synchronisation des données hors connexion dans les applications mobiles Azure]: app-service-mobile-offline-data-sync.md
[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Adding Authentication]: app-service-mobile-cordova-get-started-users.md
[authentication]: app-service-mobile-cordova-get-started-users.md
[Work with hello .NET backend server SDK for Azure Mobile Apps]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Visual Studio Community 2015]: http://www.visualstudio.com/
[Visual Studio Tools pour Apache Cordova]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[Apache Cordova SDK]: app-service-mobile-cordova-how-to-use-client-library.md
[ASP.NET Server SDK]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[Node.js Server SDK]: app-service-mobile-node-backend-how-to-use-server-sdk.md
