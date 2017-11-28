---
title: aaaEnable la synchronisation hors connexion pour votre application Mobile de Azure (Xamarin.Forms) | Documents Microsoft
description: "Découvrez comment toouse l’application Mobile App Service toocache et la synchronisation de données hors connexion dans votre application de Xamarin.Forms"
documentationcenter: xamarin
author: ggailey777
manager: yochayk
editor: 
services: app-service\mobile
ms.assetid: acf0f874-3ea5-4410-bd22-b0e72140f3b5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 10/04/2016
ms.author: glenga
ms.openlocfilehash: 4b41404fc9507e82068fdf8aa612d57cbeb366bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-xamarinforms-mobile-app"></a><span data-ttu-id="e1b76-103">Activer la synchronisation hors connexion pour votre application mobile Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="e1b76-103">Enable offline sync for your Xamarin.Forms mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="e1b76-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="e1b76-104">Overview</span></span>
<span data-ttu-id="e1b76-105">Ce didacticiel présente la fonctionnalité de synchronisation hors connexion hello des applications mobiles Azure pour Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="e1b76-105">This tutorial introduces hello offline sync feature of Azure Mobile Apps for Xamarin.Forms.</span></span> <span data-ttu-id="e1b76-106">La synchronisation hors connexion permet aux utilisateurs finaux d’interagir avec une application mobile pour afficher, ajouter ou modifier des données, même lorsqu’il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="e1b76-106">Offline sync allows end users to interact with a mobile app--viewing, adding, or modifying data--even when there is no network connection.</span></span> <span data-ttu-id="e1b76-107">Les modifications sont stockées dans une base de données locale.</span><span class="sxs-lookup"><span data-stu-id="e1b76-107">Changes are stored in a local database.</span></span> <span data-ttu-id="e1b76-108">Une fois que l’appareil de hello est remis en ligne, ces modifications sont synchronisées avec le service distant hello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-108">Once hello device is back online, these changes are synced with hello remote service.</span></span>

<span data-ttu-id="e1b76-109">Ce didacticiel est basé sur hello solution de démarrage rapide de Xamarin.Forms pour les applications mobiles que vous créez lorsque vous effectuez le didacticiel [créer une application Xamarin iOS].</span><span class="sxs-lookup"><span data-stu-id="e1b76-109">This tutorial is based on hello Xamarin.Forms quickstart solution for Mobile Apps that you create when you complete the tutorial [Create a Xamarin iOS app].</span></span> <span data-ttu-id="e1b76-110">solution de démarrage rapide de Hello pour Xamarin.Forms contient hello code toosupport synchronisation hors connexion, qui doit juste toobe activé.</span><span class="sxs-lookup"><span data-stu-id="e1b76-110">hello quickstart solution for Xamarin.Forms contains hello code toosupport offline sync, which just needs toobe enabled.</span></span> <span data-ttu-id="e1b76-111">Dans ce didacticiel, vous mettez à jour tooturn de solution de démarrage rapide de hello sur des fonctions hors connexion hello des applications mobiles Azure.</span><span class="sxs-lookup"><span data-stu-id="e1b76-111">In this tutorial, you update hello quickstart solution tooturn on hello offline features of Azure Mobile Apps.</span></span> <span data-ttu-id="e1b76-112">Nous avons également en surbrillance code hors connexion spécifiques de hello dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-112">We also highlight hello offline-specific code in hello app.</span></span> <span data-ttu-id="e1b76-113">Si vous n’utilisez pas de solution de démarrage rapide de hello téléchargé, vous devez ajouter le projet tooyour de packages d’extension hello données access.</span><span class="sxs-lookup"><span data-stu-id="e1b76-113">If you do not use hello downloaded quickstart solution, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="e1b76-114">Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure][1].</span><span class="sxs-lookup"><span data-stu-id="e1b76-114">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][1].</span></span>

<span data-ttu-id="e1b76-115">toolearn en savoir plus sur la fonctionnalité de synchronisation hors connexion hello, consultez rubrique de hello [synchronisation des données hors connexion dans les applications mobiles Azure][2].</span><span class="sxs-lookup"><span data-stu-id="e1b76-115">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="enable-offline-sync-functionality-in-hello-quickstart-solution"></a><span data-ttu-id="e1b76-116">Activer la fonctionnalité de synchronisation hors connexion dans la solution de démarrage rapide de hello</span><span class="sxs-lookup"><span data-stu-id="e1b76-116">Enable offline sync functionality in hello quickstart solution</span></span>
<span data-ttu-id="e1b76-117">code de synchronisation hors connexion Hello est inclus dans le projet de hello à l’aide de directives de préprocesseur c#.</span><span class="sxs-lookup"><span data-stu-id="e1b76-117">hello offline sync code is included in hello project by using C# preprocessor directives.</span></span> <span data-ttu-id="e1b76-118">Hello lorsque **hors connexion\_synchronisation\_activé** symbole est défini, ces chemins d’accès du code sont inclus dans la génération de hello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-118">When hello **OFFLINE\_SYNC\_ENABLED** symbol is defined, these code paths are included in hello build.</span></span> <span data-ttu-id="e1b76-119">Pour les applications Windows, vous devez également installer plateforme de SQLite hello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-119">For Windows apps, you must also install hello SQLite platform.</span></span>

1. <span data-ttu-id="e1b76-120">Dans Visual Studio, cliquez sur la solution de hello > **gérer les Packages NuGet pour la Solution...** , puis recherchez et installez le **Microsoft.Azure.Mobile.Client.SQLiteStore** package NuGet pour tous les projets dans la solution de hello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-120">In Visual Studio, right-click hello solution > **Manage NuGet Packages for Solution...**, then search for and install the **Microsoft.Azure.Mobile.Client.SQLiteStore** NuGet package for all projects in hello solution.</span></span>
2. <span data-ttu-id="e1b76-121">Bonjour l’Explorateur de solutions, ouvrez le fichier de TodoItemManager.cs de hello du projet hello avec **Portable** dans nom hello, qui est un projet de bibliothèque de classes portables, puis supprimez le commentaire hello après la directive de préprocesseur :</span><span class="sxs-lookup"><span data-stu-id="e1b76-121">In hello Solution Explorer, open hello TodoItemManager.cs file from hello project with **Portable** in hello name, which is Portable Class Library project, then uncomment hello following preprocessor directive:</span></span>

        #define OFFLINE_SYNC_ENABLED
3. <span data-ttu-id="e1b76-122">Toosupport (facultatif) les appareils Windows, installez un de hello suivant SQLite runtime packages :</span><span class="sxs-lookup"><span data-stu-id="e1b76-122">(Optional) toosupport Windows devices, install one of hello following SQLite runtime packages:</span></span>

   * <span data-ttu-id="e1b76-123">**Windows 8.1 Runtime :** installez [SQLite pour Windows 8.1][3].</span><span class="sxs-lookup"><span data-stu-id="e1b76-123">**Windows 8.1 Runtime:** Install [SQLite for Windows 8.1][3].</span></span>
   * <span data-ttu-id="e1b76-124">**Windows Phone 8.1 :** installez [SQLite pour Windows Phone 8.1][4].</span><span class="sxs-lookup"><span data-stu-id="e1b76-124">**Windows Phone 8.1:** Install [SQLite for Windows Phone 8.1][4].</span></span>
   * <span data-ttu-id="e1b76-125">**Plateforme Windows universelle** installer [SQLite pour hello Universal Windows universel][5].</span><span class="sxs-lookup"><span data-stu-id="e1b76-125">**Universal Windows Platform** Install [SQLite for hello Universal Windows Universal][5].</span></span>

     <span data-ttu-id="e1b76-126">Bien que le démarrage rapide de hello ne contient pas un projet Windows universel, plateforme Windows universelle de hello est pris en charge avec Xamarin Forms.</span><span class="sxs-lookup"><span data-stu-id="e1b76-126">Although hello quickstart does not contain a Universal Windows project, hello Universal Windows platform is supported with Xamarin Forms.</span></span>
4. <span data-ttu-id="e1b76-127">(Facultatif) Dans chaque projet d’application Windows, cliquez sur **références** > **ajouter une référence...** , développez hello **Windows** dossier > **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="e1b76-127">(Optional) In each Windows app project, right-click **References** > **Add Reference...**, expand hello **Windows** folder > **Extensions**.</span></span>
    <span data-ttu-id="e1b76-128">Activer hello approprié **SQLite pour Windows** SDK avec hello **Visual C++ Runtime pour Windows 2013** Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="e1b76-128">Enable hello appropriate **SQLite for Windows** SDK along with hello **Visual C++ 2013 Runtime for Windows** SDK.</span></span>
    <span data-ttu-id="e1b76-129">Hello SQLite SDK noms varient légèrement avec chaque plate-forme Windows.</span><span class="sxs-lookup"><span data-stu-id="e1b76-129">hello SQLite SDK names vary slightly with each Windows platform.</span></span>

## <a name="review-hello-client-sync-code"></a><span data-ttu-id="e1b76-130">Passez en revue le code de synchronisation hello client</span><span class="sxs-lookup"><span data-stu-id="e1b76-130">Review hello client sync code</span></span>
<span data-ttu-id="e1b76-131">Voici une brève vue d’ensemble de ce qui est déjà inclus dans le code hello du didacticiel à l’intérieur de hello `#if OFFLINE_SYNC_ENABLED` directives.</span><span class="sxs-lookup"><span data-stu-id="e1b76-131">Here is a brief overview of what is already included in hello tutorial code inside hello `#if OFFLINE_SYNC_ENABLED` directives.</span></span> <span data-ttu-id="e1b76-132">La fonctionnalité de synchronisation hors connexion est en fichier de projet TodoItemManager.cs hello dans le projet de bibliothèque de classes portables hello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-132">The offline sync functionality is in hello TodoItemManager.cs project file in hello Portable Class Library project.</span></span> <span data-ttu-id="e1b76-133">Pour une vue d’ensemble conceptuelle de la fonctionnalité de hello, consultez [synchronisation des données hors connexion dans les applications mobiles Azure][2].</span><span class="sxs-lookup"><span data-stu-id="e1b76-133">For a conceptual overview of hello feature, see [Offline Data Sync in Azure Mobile Apps][2].</span></span>

* <span data-ttu-id="e1b76-134">Avant de pouvoir effectuer des opérations de table, le magasin local de hello doit être initialisé.</span><span class="sxs-lookup"><span data-stu-id="e1b76-134">Before any table operations can be performed, hello local store must be initialized.</span></span> <span data-ttu-id="e1b76-135">base de données du magasin local Hello est initialisé dans hello **TodoItemManager** constructeur de classe à l’aide de hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="e1b76-135">hello local store database is initialized in hello **TodoItemManager** class constructor by using hello following code:</span></span>

        var store = new MobileServiceSQLiteStore(OfflineDbPath);
        store.DefineTable<TodoItem>();

        //Initializes hello SyncContext using hello default IMobileServiceSyncHandler.
        this.client.SyncContext.InitializeAsync(store);

        this.todoTable = client.GetSyncTable<TodoItem>();

    <span data-ttu-id="e1b76-136">Ce code crée une nouvelle base de SQLite locale à l’aide de hello **MobileServiceSQLiteStore** classe.</span><span class="sxs-lookup"><span data-stu-id="e1b76-136">This code creates a new local SQLite database using hello **MobileServiceSQLiteStore** class.</span></span>

    <span data-ttu-id="e1b76-137">Hello **DefineTable** méthode crée une table dans le magasin local hello qui correspond aux champs hello dans le type de hello fourni.</span><span class="sxs-lookup"><span data-stu-id="e1b76-137">hello **DefineTable** method creates a table in hello local store that matches hello fields in hello provided type.</span></span>  <span data-ttu-id="e1b76-138">type de Hello ne tooinclude toutes les colonnes hello qui se trouvent dans la base de données distante hello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-138">hello type doesn't have tooinclude all hello columns that are in hello remote database.</span></span> <span data-ttu-id="e1b76-139">Il est possible de toostore un sous-ensemble de colonnes.</span><span class="sxs-lookup"><span data-stu-id="e1b76-139">It is possible toostore a subset of columns.</span></span>
* <span data-ttu-id="e1b76-140">Hello **todoTable** champ **TodoItemManager** est un **IMobileServiceSyncTable** de type au lieu de **IMobileServiceTable**.</span><span class="sxs-lookup"><span data-stu-id="e1b76-140">hello **todoTable** field in **TodoItemManager** is an **IMobileServiceSyncTable** type instead of **IMobileServiceTable**.</span></span> <span data-ttu-id="e1b76-141">Cette classe utilise hello base de données locale pour tous les créer, lire, mettre à jour et supprimer (CRUD) des opérations de table.</span><span class="sxs-lookup"><span data-stu-id="e1b76-141">This class uses hello local database for all create, read, update, and delete (CRUD) table operations.</span></span> <span data-ttu-id="e1b76-142">Vous décidez lorsque ces modifications sont envoyées principal de l’application Mobile toohello en appelant **PushAsync** sur hello **IMobileServiceSyncContext**.</span><span class="sxs-lookup"><span data-stu-id="e1b76-142">You decide when those changes are pushed toohello Mobile App backend by calling **PushAsync** on hello **IMobileServiceSyncContext**.</span></span> <span data-ttu-id="e1b76-143">Hello contexte de synchronisation permet de conserver les relations entre les tables en effectuant le suivi en exécutant un push des modifications dans une application cliente a modifié lors de toutes les tables **PushAsync** est appelée.</span><span class="sxs-lookup"><span data-stu-id="e1b76-143">hello sync context helps preserve table relationships by tracking and pushing changes in all tables a client app has modified when **PushAsync** is called.</span></span>

    <span data-ttu-id="e1b76-144">suivant de Hello **SyncAsync** méthode est appelée toosync avec le serveur principal de l’application Mobile hello :</span><span class="sxs-lookup"><span data-stu-id="e1b76-144">hello following **SyncAsync** method is called toosync with hello Mobile App backend:</span></span>

        public async Task SyncAsync()
        {
            ReadOnlyCollection<MobileServiceTableOperationError> syncErrors = null;

            try
            {
                await this.client.SyncContext.PushAsync();

                await this.todoTable.PullAsync(
                    "allTodoItems",
                    this.todoTable.CreateQuery());
            }
            catch (MobileServicePushFailedException exc)
            {
                if (exc.PushResult != null)
                {
                    syncErrors = exc.PushResult.Errors;
                }
            }

            // Simple error/conflict handling.
            if (syncErrors != null)
            {
                foreach (var error in syncErrors)
                {
                    if (error.OperationKind == MobileServiceTableOperationKind.Update && error.Result != null)
                    {
                        //Update failed, reverting tooserver's copy.
                        await error.CancelAndUpdateItemAsync(error.Result);
                    }
                    else
                    {
                        // Discard local change.
                        await error.CancelAndDiscardItemAsync();
                    }

                    Debug.WriteLine(@"Error executing sync operation. Item: {0} ({1}). Operation discarded.",
                        error.TableName, error.Item["id"]);
                }
            }
        }

    <span data-ttu-id="e1b76-145">Cet exemple utilise la simple gestion des erreurs avec Gestionnaire de synchronisation par défaut hello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-145">This sample uses simple error handling with hello default sync handler.</span></span> <span data-ttu-id="e1b76-146">Une application réelle traiterait hello diverses erreurs telles que les conditions du réseau et le serveur est en conflit à l’aide d’un **IMobileServiceSyncHandler** mise en œuvre.</span><span class="sxs-lookup"><span data-stu-id="e1b76-146">A real application would handle hello various errors like network conditions and server conflicts by using a custom **IMobileServiceSyncHandler** implementation.</span></span>

## <a name="offline-sync-considerations"></a><span data-ttu-id="e1b76-147">Considérations relatives à la synchronisation hors connexion</span><span class="sxs-lookup"><span data-stu-id="e1b76-147">Offline sync considerations</span></span>
<span data-ttu-id="e1b76-148">Dans l’exemple hello, hello **SyncAsync** méthode est appelée uniquement sur la mise en route et lorsqu’une synchronisation est demandée.</span><span class="sxs-lookup"><span data-stu-id="e1b76-148">In hello sample, hello **SyncAsync** method is only called on start-up and when a sync is requested.</span></span>  <span data-ttu-id="e1b76-149">tooinitiate une synchronisation dans une application Android ou iOS, par extraction vers le bas sur la liste des éléments hello ; pour Windows, utilisez hello **synchronisation** bouton.</span><span class="sxs-lookup"><span data-stu-id="e1b76-149">tooinitiate a sync in an Android or iOS app, pull down on hello items list; for Windows, use hello **Sync** button.</span></span> <span data-ttu-id="e1b76-150">Dans une application réelle, vous pouvez également apporter des déclencheurs de synchronisation hello lorsque l’état hello réseau change.</span><span class="sxs-lookup"><span data-stu-id="e1b76-150">In a real-world application, you could also make hello sync trigger when hello network state changes.</span></span>

<span data-ttu-id="e1b76-151">Lorsqu’une extraction est exécutée sur une table qui comporte en attente mises à jour locales suivies par le contexte de hello, qui extrait les opération automatiquement les déclencheurs de push de contexte précédent.</span><span class="sxs-lookup"><span data-stu-id="e1b76-151">When a pull is executed against a table that has pending local updates tracked by hello context, that pull operation automatically triggers a preceding context push.</span></span> <span data-ttu-id="e1b76-152">Lors de l’actualisation, l’ajout et la fin des éléments dans cet exemple, vous pouvez omettre hello explicite **PushAsync** appeler.</span><span class="sxs-lookup"><span data-stu-id="e1b76-152">When refreshing, adding, and completing items in this sample, you can omit hello explicit **PushAsync** call.</span></span>

<span data-ttu-id="e1b76-153">Dans le code hello fourni, tous les enregistrements dans la table TodoItem à distance de hello sont interrogées, mais il est également possible de toofilter enregistrements en passant un id de requête et une requête trop**PushAsync**.</span><span class="sxs-lookup"><span data-stu-id="e1b76-153">In hello provided code, all records in hello remote TodoItem table are queried, but it is also possible toofilter records by passing a query id and query too**PushAsync**.</span></span> <span data-ttu-id="e1b76-154">Pour plus d’informations, consultez la section de hello *synchronisation incrémentielle* dans [synchronisation des données hors connexion dans les applications mobiles Azure][2].</span><span class="sxs-lookup"><span data-stu-id="e1b76-154">For more information, see hello section *Incremental Sync* in [Offline Data Sync in Azure Mobile Apps][2].</span></span>

## <a name="run-hello-client-app"></a><span data-ttu-id="e1b76-155">Exécuter l’application cliente de hello</span><span class="sxs-lookup"><span data-stu-id="e1b76-155">Run hello client app</span></span>
<span data-ttu-id="e1b76-156">Avec la synchronisation hors connexion est maintenant activée, exécutez application cliente de hello au moins une fois sur chaque base de données de plateforme toopopulate hello magasin local.</span><span class="sxs-lookup"><span data-stu-id="e1b76-156">With offline sync now enabled, run hello client application at least once on each platform toopopulate hello local store database.</span></span> <span data-ttu-id="e1b76-157">Une version ultérieure, de simuler un scénario hors connexion et de modifier des données de hello dans le magasin local de hello lors de l’application hello est hors connexion.</span><span class="sxs-lookup"><span data-stu-id="e1b76-157">Later, simulate an offline scenario and modify hello data in hello local store while hello app is offline.</span></span>

## <a name="update-hello-sync-behavior-of-hello-client-app"></a><span data-ttu-id="e1b76-158">Mettre à jour le comportement de synchronisation hello de hello client application</span><span class="sxs-lookup"><span data-stu-id="e1b76-158">Update hello sync behavior of hello client app</span></span>
<span data-ttu-id="e1b76-159">Dans cette section, modifiez hello client projet toosimulate un scénario hors connexion à l’aide d’une URL d’application non valide pour votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="e1b76-159">In this section, modify hello client project toosimulate an offline scenario by using an invalid application URL for your backend.</span></span> <span data-ttu-id="e1b76-160">Ou bien, vous pouvez désactiver les connexions réseau en déplaçant votre appareil trop « Mode avion ».</span><span class="sxs-lookup"><span data-stu-id="e1b76-160">Alternatively, you can turn off network connections by moving your device too"Airplane mode."</span></span>  <span data-ttu-id="e1b76-161">Lorsque vous ajoutez ou modifiez des éléments de données, ces modifications sont conservées dans le magasin local de hello, mais non synchronisées du magasin de données de serveur principal toohello jusqu'à ce que la connexion de hello est rétablie.</span><span class="sxs-lookup"><span data-stu-id="e1b76-161">When you add or change data items, these changes are held in hello local store, but not synced toohello backend data store until hello connection is re-established.</span></span>

1. <span data-ttu-id="e1b76-162">Bonjour l’Explorateur de solutions, ouvrez le fichier de projet de Constants.cs de hello de hello **Portable** de projet et modifier la valeur hello `ApplicationURL` URL non valide de toopoint tooan :</span><span class="sxs-lookup"><span data-stu-id="e1b76-162">In hello Solution Explorer, open hello Constants.cs project file from hello **Portable** project and change hello value of `ApplicationURL` toopoint tooan invalid URL:</span></span>

        public static string ApplicationURL = @"https://your-service.azurewebsites.net/";
2. <span data-ttu-id="e1b76-163">Fichier ouvert hello TodoItemManager.cs hello **Portable** de projet, puis ajoutez un **catch** pour hello base **Exception** toohello de la classe **try... catch** bloquer **SyncAsync**.</span><span class="sxs-lookup"><span data-stu-id="e1b76-163">Open hello TodoItemManager.cs file from hello **Portable** project, then add a **catch** for hello base **Exception** class toohello **try...catch** block in **SyncAsync**.</span></span> <span data-ttu-id="e1b76-164">Cela **catch** bloc écrit hello exception message toohello la console, comme suit :</span><span class="sxs-lookup"><span data-stu-id="e1b76-164">This **catch** block writes hello exception message toohello console, as follows:</span></span>

            catch (Exception ex)
            {
                Console.Error.WriteLine(@"Exception: {0}", ex.Message);
            }
3. <span data-ttu-id="e1b76-165">Générez et exécutez l’application cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-165">Build and run hello client app.</span></span>  <span data-ttu-id="e1b76-166">Ajoutez de nouveaux éléments.</span><span class="sxs-lookup"><span data-stu-id="e1b76-166">Add some new items.</span></span> <span data-ttu-id="e1b76-167">Notez qu’une exception est enregistrée dans la console hello pour chaque toosync tentative avec le serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-167">Notice that an exception is logged in hello console for each attempt toosync with hello backend.</span></span> <span data-ttu-id="e1b76-168">Ces nouveaux éléments existent uniquement dans le magasin local de hello jusqu'à ce qu’elles peuvent être appliquées backend mobile de toohello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-168">These new items exist only in hello local store until they can be pushed toohello mobile backend.</span></span> <span data-ttu-id="e1b76-169">Hello client application se comporte comme si elle était toohello connecté principal, la prise en charge que tous les créent, lire, la mise à jour, les opérations de suppression (CRUD).</span><span class="sxs-lookup"><span data-stu-id="e1b76-169">hello client app behaves as if it is connected toohello backend, supporting all create, read, update, delete (CRUD) operations.</span></span>
4. <span data-ttu-id="e1b76-170">Fermez l’application hello et redémarrez-le tooverify que hello nouveaux éléments que vous avez créé sont magasin local de toohello persistante.</span><span class="sxs-lookup"><span data-stu-id="e1b76-170">Close hello app and restart it tooverify that hello new items you created are persisted toohello local store.</span></span>
5. <span data-ttu-id="e1b76-171">(Facultatif) Utilisez Visual Studio tooview votre toosee de table de base de données SQL Azure données hello dans la base de données principale hello n’a pas changé.</span><span class="sxs-lookup"><span data-stu-id="e1b76-171">(Optional) Use Visual Studio tooview your Azure SQL Database table toosee that hello data in hello backend database has not changed.</span></span>

    <span data-ttu-id="e1b76-172">Dans Visual Studio, ouvrez l' **Explorateur de serveurs**.</span><span class="sxs-lookup"><span data-stu-id="e1b76-172">In Visual Studio, open **Server Explorer**.</span></span> <span data-ttu-id="e1b76-173">Accédez de la base de données tooyour dans **Azure**->**bases de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="e1b76-173">Navigate tooyour database in **Azure**->**SQL Databases**.</span></span> <span data-ttu-id="e1b76-174">Cliquez avec le bouton droit sur votre base de données, puis sélectionnez **Ouvrir dans l’Explorateur d’objets SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="e1b76-174">Right-click your database and select **Open in SQL Server Object Explorer**.</span></span> <span data-ttu-id="e1b76-175">Vous pouvez maintenant rechercher table de base de données SQL tooyour et son contenu.</span><span class="sxs-lookup"><span data-stu-id="e1b76-175">Now you can browse tooyour SQL database table and its contents.</span></span>

## <a name="update-hello-client-app-tooreconnect-your-mobile-backend"></a><span data-ttu-id="e1b76-176">Mettre à jour hello client application tooreconnect votre serveur principal mobile</span><span class="sxs-lookup"><span data-stu-id="e1b76-176">Update hello client app tooreconnect your mobile backend</span></span>
<span data-ttu-id="e1b76-177">Dans cette section, vous reconnecter hello toohello mobile serveur principal d’application, qui simule l’application hello fidéliser tooan des état en ligne.</span><span class="sxs-lookup"><span data-stu-id="e1b76-177">In this section, reconnect hello app toohello mobile backend, which simulates hello app coming back tooan online state.</span></span> <span data-ttu-id="e1b76-178">Lorsque vous effectuez le mouvement d’actualisation hello, les données sont synchronisés tooyour les backend mobile.</span><span class="sxs-lookup"><span data-stu-id="e1b76-178">When you perform hello refresh gesture, data is synced tooyour mobile backend.</span></span>

1. <span data-ttu-id="e1b76-179">Rouvrez Constants.cs.</span><span class="sxs-lookup"><span data-stu-id="e1b76-179">Reopen Constants.cs.</span></span> <span data-ttu-id="e1b76-180">Hello correct `applicationURL` toopoint toohello Corrigez-la.</span><span class="sxs-lookup"><span data-stu-id="e1b76-180">Correct hello `applicationURL` toopoint toohello correct URL.</span></span>
2. <span data-ttu-id="e1b76-181">Regénérez et exécutez l’application cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-181">Rebuild and run hello client app.</span></span> <span data-ttu-id="e1b76-182">application Hello tentatives toosync avec le serveur principal d’application mobile hello après le lancement.</span><span class="sxs-lookup"><span data-stu-id="e1b76-182">hello app attempts toosync with hello mobile app backend after launching.</span></span> <span data-ttu-id="e1b76-183">Vérifiez qu’aucune exceptions ne sont enregistrées dans la console de débogage hello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-183">Verify that no exceptions are logged in hello debug console.</span></span>
3. <span data-ttu-id="e1b76-184">(Facultatif) Hello d’affichage mis à jour les données à l’aide de l’Explorateur d’objets SQL Server ou d’un outil REST, comme Fiddler ou [Postman][6].</span><span class="sxs-lookup"><span data-stu-id="e1b76-184">(Optional) View hello updated data using either SQL Server Object Explorer or a REST tool like Fiddler or [Postman][6].</span></span> <span data-ttu-id="e1b76-185">Les données de salutation avis a été synchronisées entre la base de données principale hello et magasin local de hello.</span><span class="sxs-lookup"><span data-stu-id="e1b76-185">Notice hello data has been synchronized between hello backend database and hello local store.</span></span>

    <span data-ttu-id="e1b76-186">Notez que les données de salutation a été synchronisées entre la base de données hello et magasin local de hello et contient les éléments hello que vous avez ajouté pendant que votre application a été déconnectée.</span><span class="sxs-lookup"><span data-stu-id="e1b76-186">Notice hello data has been synchronized between hello database and hello local store and contains hello items you added while your app was disconnected.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1b76-187">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e1b76-187">Additional Resources</span></span>
* <span data-ttu-id="e1b76-188">[Synchronisation des données hors connexion dans Azure Mobile Apps][2]</span><span class="sxs-lookup"><span data-stu-id="e1b76-188">[Offline Data Sync in Azure Mobile Apps][2]</span></span>
* <span data-ttu-id="e1b76-189">[SDK HOWTO Azure Mobile Apps .NET][8]</span><span class="sxs-lookup"><span data-stu-id="e1b76-189">[Azure Mobile Apps .NET SDK HOWTO][8]</span></span>

<!-- URLs. -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: app-service-mobile-offline-data-sync.md
[3]: http://go.microsoft.com/fwlink/p/?LinkID=716919
[4]: http://go.microsoft.com/fwlink/p/?LinkID=716920
[5]: http://sqlite.org/2016/sqlite-uwp-3120200.vsix
[6]: https://www.getpostman.com/
[7]: http://www.telerik.com/fiddler
[8]: app-service-mobile-dotnet-how-to-use-client-library.md
