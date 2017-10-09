---
title: aaaEnable la synchronisation hors connexion pour votre application Mobile de Azure (Android)
description: "Découvrez comment toouse App Service Mobile Apps toocache et la synchronisation de données hors connexion dans votre application Android"
documentationcenter: android
author: ggailey777
manager: syntaxc4
services: app-service\mobile
ms.assetid: 32a8a079-9b3c-4faf-8588-ccff02097224
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 34508c7394610cf9127e1753637940826b8fd06a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="d8d52-103">Activation de la synchronisation hors connexion pour votre application mobile Android</span><span class="sxs-lookup"><span data-stu-id="d8d52-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="d8d52-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d8d52-104">Overview</span></span>
<span data-ttu-id="d8d52-105">Ce didacticiel décrit la fonctionnalité de synchronisation hors connexion hello des applications mobiles Azure pour Android.</span><span class="sxs-lookup"><span data-stu-id="d8d52-105">This tutorial covers hello offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="d8d52-106">Synchronisation hors connexion permet toointeract des utilisateurs finaux avec une application mobile&mdash;affichage, l’ajout ou la modification des données&mdash;même quand il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="d8d52-106">Offline sync allows end users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="d8d52-107">Les modifications sont stockées dans une base de données locale.</span><span class="sxs-lookup"><span data-stu-id="d8d52-107">Changes are stored in a local database.</span></span> <span data-ttu-id="d8d52-108">Une fois que l’appareil de hello est remis en ligne, ces modifications sont synchronisées avec le serveur principal à distance hello.</span><span class="sxs-lookup"><span data-stu-id="d8d52-108">Once hello device is back online, these changes are synced with hello remote backend.</span></span>

<span data-ttu-id="d8d52-109">S’il s’agit de votre première expérience avec les applications mobiles Azure, vous devez d’abord terminer didacticiel de hello [créer une application Android].</span><span class="sxs-lookup"><span data-stu-id="d8d52-109">If this is your first experience with Azure Mobile Apps, you should first complete hello tutorial [Create an Android App].</span></span> <span data-ttu-id="d8d52-110">Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez ajouter projet tooyour de packages d’extension hello données access.</span><span class="sxs-lookup"><span data-stu-id="d8d52-110">If you do not use hello downloaded quick start server project, you must add hello data access extension packages tooyour project.</span></span> <span data-ttu-id="d8d52-111">Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d8d52-111">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="d8d52-112">toolearn en savoir plus sur la fonctionnalité de synchronisation hors connexion hello, consultez rubrique de hello [synchronisation des données hors connexion dans les applications mobiles Azure].</span><span class="sxs-lookup"><span data-stu-id="d8d52-112">toolearn more about hello offline sync feature, see hello topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-hello-app-toosupport-offline-sync"></a><span data-ttu-id="d8d52-113">Mettre à jour de la synchronisation hors connexion des toosupport application hello</span><span class="sxs-lookup"><span data-stu-id="d8d52-113">Update hello app toosupport offline sync</span></span>
<span data-ttu-id="d8d52-114">Avec la synchronisation hors connexion, vous lecture/écriture de tooand à partir d’un *table de synchronisation* (à l’aide de hello *IMobileServiceSyncTable* interface), qui fait partie d’un **SQLite** base de données sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d8d52-114">With offline sync, you read tooand write from a *sync table* (using hello *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="d8d52-115">les modifications toopush et par extraction de données entre les périphériques hello et Azure Mobile Services, vous utilisez un *contexte de synchronisation* (*MobileServiceClient.SyncContext*), qui vous initialisez avec la base de données locale hello données toostore localement.</span><span class="sxs-lookup"><span data-stu-id="d8d52-115">toopush and pull changes between hello device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with hello local database toostore data locally.</span></span>

1. <span data-ttu-id="d8d52-116">Dans `TodoActivity.java`, commentez la définition existante de hello de `mToDoTable` et supprimez les commentaires de version de la table hello synchronisation :</span><span class="sxs-lookup"><span data-stu-id="d8d52-116">In `TodoActivity.java`, comment out hello existing definition of `mToDoTable` and uncomment hello sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="d8d52-117">Bonjour `onCreate` méthode, commentez l’initialisation d’existant hello de `mToDoTable` et supprimez les commentaires de cette définition :</span><span class="sxs-lookup"><span data-stu-id="d8d52-117">In hello `onCreate` method, comment out hello existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="d8d52-118">Dans `refreshItemsFromTable` Commentez la définition de hello de `results` et supprimez les commentaires de cette définition :</span><span class="sxs-lookup"><span data-stu-id="d8d52-118">In `refreshItemsFromTable` comment out hello definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="d8d52-119">Commentez la définition de hello de `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="d8d52-119">Comment out hello definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="d8d52-120">Supprimez les commentaires de la définition de hello de `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="d8d52-120">Uncomment hello definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync hello data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="d8d52-121">Supprimez les commentaires de la définition de hello de `sync`:</span><span class="sxs-lookup"><span data-stu-id="d8d52-121">Uncomment hello definition of `sync`:</span></span>
   
        private AsyncTask<Void, Void, Void> sync() {
            AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
                @Override
                protected Void doInBackground(Void... params) {
                    try {
                        MobileServiceSyncContext syncContext = mClient.getSyncContext();
                        syncContext.push().get();
                        mToDoTable.pull(null).get();
                    } catch (final Exception e) {
                        createAndShowDialogFromTask(e, "Error");
                    }
                    return null;
                }
            };
            return runAsyncTask(task);
        }

## <a name="test-hello-app"></a><span data-ttu-id="d8d52-122">Application de test hello</span><span class="sxs-lookup"><span data-stu-id="d8d52-122">Test hello app</span></span>
<span data-ttu-id="d8d52-123">Dans cette section, vous testez le comportement de hello avec Wi-Fi sur et mettez hors tension Wi-Fi toocreate un scénario hors connexion.</span><span class="sxs-lookup"><span data-stu-id="d8d52-123">In this section, you test hello behavior with WiFi on, and then turn off WiFi toocreate an offline scenario.</span></span>

<span data-ttu-id="d8d52-124">Lorsque vous ajoutez des éléments de données, elles sont conservées dans le magasin de SQLite hello local, mais pas synchronisés toohello des services mobiles jusqu'à ce que vous appuyez sur hello **Actualiser** bouton.</span><span class="sxs-lookup"><span data-stu-id="d8d52-124">When you add data items, they are held in hello local SQLite store, but not synced toohello mobile service until you press hello **Refresh** button.</span></span> <span data-ttu-id="d8d52-125">Autres applications peuvent avoir des exigences différentes concernant lorsque les données doivent toobe synchronisé, mais à des fins de démonstration ce didacticiel propose hello demander explicitement.</span><span class="sxs-lookup"><span data-stu-id="d8d52-125">Other apps may have different requirements regarding when data needs toobe synchronized, but for demo purposes this tutorial has hello user explicitly request it.</span></span>

<span data-ttu-id="d8d52-126">Lorsque vous appuyez sur ce bouton, une nouvelle tâche en arrière-plan démarre.</span><span class="sxs-lookup"><span data-stu-id="d8d52-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="d8d52-127">Il transmet d’abord toutes les modifications apportées toohello magasin local à l’aide du contexte de synchronisation, puis extrait tous les modifié des données à partir de la table locale de toohello Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d52-127">It first pushes all changes made toohello local store using synchronization context, then pulls all changed data from Azure toohello local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="d8d52-128">Test hors connexion</span><span class="sxs-lookup"><span data-stu-id="d8d52-128">Offline testing</span></span>
1. <span data-ttu-id="d8d52-129">Appareil de hello sur place ou le simulateur dans *Mode avion*.</span><span class="sxs-lookup"><span data-stu-id="d8d52-129">Place hello device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="d8d52-130">Cela crée un scénario hors connexion.</span><span class="sxs-lookup"><span data-stu-id="d8d52-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="d8d52-131">Ajoutez des *tâches* , ou marquez-en certaines comme terminées.</span><span class="sxs-lookup"><span data-stu-id="d8d52-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="d8d52-132">Quittez hello appareil ou simulateur (ou application hello fermeture forcée) et redémarrez.</span><span class="sxs-lookup"><span data-stu-id="d8d52-132">Quit hello device or simulator (or forcibly close hello app) and restart.</span></span> <span data-ttu-id="d8d52-133">Vérifiez que vos modifications ont été rendues persistantes sur l’appareil de hello, car ils sont conservés dans le magasin de SQLite hello local.</span><span class="sxs-lookup"><span data-stu-id="d8d52-133">Verify that your changes have been persisted on hello device because they are held in hello local SQLite store.</span></span>
3. <span data-ttu-id="d8d52-134">Afficher le contenu de hello Hello Azure *TodoItem* telles que la table avec un outil SQL *SQL Server Management Studio*, ou un client REST comme *Fiddler* ou  *Postman*.</span><span class="sxs-lookup"><span data-stu-id="d8d52-134">View hello contents of hello Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="d8d52-135">Vérifiez que de nouveaux éléments de hello *pas* été synchronisés toohello server</span><span class="sxs-lookup"><span data-stu-id="d8d52-135">Verify that hello new items have *not* been synced toohello server</span></span>
   
       + <span data-ttu-id="d8d52-136">Pour un service principal Node.js, consultez toohello [portail Azure](https://portal.azure.com/), dans votre application Mobile sur principal **Tables facile** > **TodoItem** contenu de hello tooview Hello `TodoItem` table.</span><span class="sxs-lookup"><span data-stu-id="d8d52-136">For a Node.js backend, go toohello [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** tooview hello contents of hello `TodoItem` table.</span></span>
       + <span data-ttu-id="d8d52-137">Pour un service principal .NET, table hello d’affichage de contenu avec un outil SQL comme *SQL Server Management Studio*, ou un client REST comme *Fiddler* ou *Postman*.</span><span class="sxs-lookup"><span data-stu-id="d8d52-137">For a .NET backend, view hello table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="d8d52-138">Activer Wi-Fi dans le simulateur ou l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="d8d52-138">Turn on WiFi in hello device or simulator.</span></span> <span data-ttu-id="d8d52-139">Ensuite, appuyez sur hello **Actualiser** bouton.</span><span class="sxs-lookup"><span data-stu-id="d8d52-139">Next, press hello **Refresh** button.</span></span>
5. <span data-ttu-id="d8d52-140">Affichez de nouveau les données de salutation TodoItem Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d8d52-140">View hello TodoItem data again in hello Azure portal.</span></span> <span data-ttu-id="d8d52-141">Hello que nouvelles et modifiées TodoItems doit maintenant apparaître.</span><span class="sxs-lookup"><span data-stu-id="d8d52-141">hello new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8d52-142">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d8d52-142">Additional Resources</span></span>
* <span data-ttu-id="d8d52-143">[synchronisation des données hors connexion dans les applications mobiles Azure]</span><span class="sxs-lookup"><span data-stu-id="d8d52-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="d8d52-144">[Couverture du cloud : La synchronisation hors connexion dans Services mobiles Azure] \(Remarque : hello vidéo se trouve sur les Services mobiles, mais la synchronisation hors connexion fonctionne de façon similaire dans les applications mobiles Azure\)</span><span class="sxs-lookup"><span data-stu-id="d8d52-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: hello video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

[synchronisation des données hors connexion dans les applications mobiles Azure]: app-service-mobile-offline-data-sync.md

[créer une application Android]: app-service-mobile-android-get-started.md

[Couverture du cloud : La synchronisation hors connexion dans Services mobiles Azure]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

