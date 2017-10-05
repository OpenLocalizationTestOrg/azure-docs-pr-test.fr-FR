---
title: Activation de la synchronisation hors connexion pour votre application Azure Mobile App (Android)
description: "Découvrez comment utiliser Service Mobile App pour mettre en cache et synchroniser des données hors connexion dans votre application Android"
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
ms.openlocfilehash: 304323c1816302e8c1f68f36a029aee55e02c54e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="enable-offline-sync-for-your-android-mobile-app"></a><span data-ttu-id="d43dc-103">Activation de la synchronisation hors connexion pour votre application mobile Android</span><span class="sxs-lookup"><span data-stu-id="d43dc-103">Enable offline sync for your Android mobile app</span></span>
[!INCLUDE [app-service-mobile-selector-offline](../../includes/app-service-mobile-selector-offline.md)]

## <a name="overview"></a><span data-ttu-id="d43dc-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="d43dc-104">Overview</span></span>
<span data-ttu-id="d43dc-105">Ce didacticiel traite de la fonctionnalité de synchronisation hors connexion d’Azure Mobile Apps pour Android.</span><span class="sxs-lookup"><span data-stu-id="d43dc-105">This tutorial covers the offline sync feature of Azure Mobile Apps for Android.</span></span> <span data-ttu-id="d43dc-106">La synchronisation hors connexion permet aux utilisateurs finaux d’interagir avec une application mobile &mdash;pour afficher, ajouter ou modifier des données&mdash;, même lorsqu’il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="d43dc-106">Offline sync allows end users to interact with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span> <span data-ttu-id="d43dc-107">Les modifications sont stockées dans une base de données locale.</span><span class="sxs-lookup"><span data-stu-id="d43dc-107">Changes are stored in a local database.</span></span> <span data-ttu-id="d43dc-108">Une fois l'appareil de nouveau en ligne, ces modifications sont synchronisées avec le serveur principal distant.</span><span class="sxs-lookup"><span data-stu-id="d43dc-108">Once the device is back online, these changes are synced with the remote backend.</span></span>

<span data-ttu-id="d43dc-109">Si vous n’avez aucune expérience d’Azure Mobile Apps, vous devez commencer par suivre le didacticiel [Création d’une application Android].</span><span class="sxs-lookup"><span data-stu-id="d43dc-109">If this is your first experience with Azure Mobile Apps, you should first complete the tutorial [Create an Android App].</span></span> <span data-ttu-id="d43dc-110">Si vous n’utilisez pas le projet de serveur du démarrage rapide téléchargé, vous devez ajouter les packages d’extension d’accès aux données à votre projet.</span><span class="sxs-lookup"><span data-stu-id="d43dc-110">If you do not use the downloaded quick start server project, you must add the data access extension packages to your project.</span></span> <span data-ttu-id="d43dc-111">Pour plus d'informations sur les packages d'extension de serveur, consultez [Fonctionnement avec le Kit de développement logiciel (SDK) du serveur principal .NET pour Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="d43dc-111">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

<span data-ttu-id="d43dc-112">Pour plus d’informations sur la fonctionnalité de synchronisation hors connexion, consultez la rubrique [Synchronisation des données hors connexion dans Azure Mobile Apps].</span><span class="sxs-lookup"><span data-stu-id="d43dc-112">To learn more about the offline sync feature, see the topic [Offline Data Sync in Azure Mobile Apps].</span></span>

## <a name="update-the-app-to-support-offline-sync"></a><span data-ttu-id="d43dc-113">Mettre à jour l’application pour prendre en charge la synchronisation hors connexion</span><span class="sxs-lookup"><span data-stu-id="d43dc-113">Update the app to support offline sync</span></span>
<span data-ttu-id="d43dc-114">Avec la synchronisation hors connexion, vous disposez d’un accès en lecture et en écriture à partir d’une *table de synchronisation* (à l’aide de l’interface *IMobileServiceSyncTable*), qui fait partie d’une base de données **SQLite** sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="d43dc-114">With offline sync, you read to and write from a *sync table* (using the *IMobileServiceSyncTable* interface), which is part of a **SQLite** database on your device.</span></span>

<span data-ttu-id="d43dc-115">Pour envoyer et extraire des modifications entre l’appareil et Azure Mobile Services, faites appel à un *contexte de synchronisation* (*MobileServiceClient.SyncContext*), que vous initialisez avec la base de données locale utilisée pour stocker des données localement.</span><span class="sxs-lookup"><span data-stu-id="d43dc-115">To push and pull changes between the device and Azure Mobile Services, you use a *synchronization context* (*MobileServiceClient.SyncContext*), which you initialize with the local database to store data locally.</span></span>

1. <span data-ttu-id="d43dc-116">Dans `TodoActivity.java`, commentez la définition existante de `mToDoTable` et supprimez les marques de commentaires de la version de table de synchronisation :</span><span class="sxs-lookup"><span data-stu-id="d43dc-116">In `TodoActivity.java`, comment out the existing definition of `mToDoTable` and uncomment the sync table version:</span></span>
   
        private MobileServiceSyncTable<ToDoItem> mToDoTable;
2. <span data-ttu-id="d43dc-117">Dans la méthode `onCreate`, commentez l’initialisation existante de `mToDoTable` et supprimez les marques de commentaires de cette définition :</span><span class="sxs-lookup"><span data-stu-id="d43dc-117">In the `onCreate` method, comment out the existing initialization of `mToDoTable` and uncomment this definition:</span></span>
   
        mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
3. <span data-ttu-id="d43dc-118">Dans `refreshItemsFromTable` commentez la définition de `results` et supprimez les marque de commentaires de cette définition :</span><span class="sxs-lookup"><span data-stu-id="d43dc-118">In `refreshItemsFromTable` comment out the definition of `results` and uncomment this definition:</span></span>
   
        // Offline Sync
        final List<ToDoItem> results = refreshItemsFromMobileServiceTableSyncTable();
4. <span data-ttu-id="d43dc-119">Commentez la définition de `refreshItemsFromMobileServiceTable`.</span><span class="sxs-lookup"><span data-stu-id="d43dc-119">Comment out the definition of `refreshItemsFromMobileServiceTable`.</span></span>
5. <span data-ttu-id="d43dc-120">Supprimez les marques de commentaires de la définition de `refreshItemsFromMobileServiceTableSyncTable`:</span><span class="sxs-lookup"><span data-stu-id="d43dc-120">Uncomment the definition of `refreshItemsFromMobileServiceTableSyncTable`:</span></span>
   
        private List<ToDoItem> refreshItemsFromMobileServiceTableSyncTable() throws ExecutionException, InterruptedException {
            //sync the data
            sync().get();
            Query query = QueryOperations.field("complete").
                    eq(val(false));
            return mToDoTable.read(query).get();
        }
6. <span data-ttu-id="d43dc-121">Supprimez les marques de commentaires de la définition de `sync`:</span><span class="sxs-lookup"><span data-stu-id="d43dc-121">Uncomment the definition of `sync`:</span></span>
   
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

## <a name="test-the-app"></a><span data-ttu-id="d43dc-122">Test de l'application</span><span class="sxs-lookup"><span data-stu-id="d43dc-122">Test the app</span></span>
<span data-ttu-id="d43dc-123">Dans cette section, vous testez le comportement de l’application avec le Wi-Fi activé, puis vous désactivez le Wi-Fi pour créer un scénario hors connexion.</span><span class="sxs-lookup"><span data-stu-id="d43dc-123">In this section, you test the behavior with WiFi on, and then turn off WiFi to create an offline scenario.</span></span>

<span data-ttu-id="d43dc-124">Lorsque vous ajoutez des éléments de données, ils sont stockés dans le magasin local SQLite, mais ils ne sont synchronisés avec le service mobile que si vous appuyez sur le bouton **Actualiser** .</span><span class="sxs-lookup"><span data-stu-id="d43dc-124">When you add data items, they are held in the local SQLite store, but not synced to the mobile service until you press the **Refresh** button.</span></span> <span data-ttu-id="d43dc-125">D’autres applications peuvent avoir des besoins différents concernant la fréquence de synchronisation des données, mais à des fins de démonstration, l’utilisateur doit en faire explicitement la requête dans le cadre de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="d43dc-125">Other apps may have different requirements regarding when data needs to be synchronized, but for demo purposes this tutorial has the user explicitly request it.</span></span>

<span data-ttu-id="d43dc-126">Lorsque vous appuyez sur ce bouton, une nouvelle tâche en arrière-plan démarre.</span><span class="sxs-lookup"><span data-stu-id="d43dc-126">When you press that button, a new background task starts.</span></span> <span data-ttu-id="d43dc-127">Elle commence par transmettre toutes les modifications apportées dans le magasin local à l’aide du contexte de synchronisation, puis extrait tous les données modifiées à partir d’Azure vers la table locale.</span><span class="sxs-lookup"><span data-stu-id="d43dc-127">It first pushes all changes made to the local store using synchronization context, then pulls all changed data from Azure to the local table.</span></span>

### <a name="offline-testing"></a><span data-ttu-id="d43dc-128">Test hors connexion</span><span class="sxs-lookup"><span data-stu-id="d43dc-128">Offline testing</span></span>
1. <span data-ttu-id="d43dc-129">Mettez l’appareil ou le simulateur en *Mode avion*.</span><span class="sxs-lookup"><span data-stu-id="d43dc-129">Place the device or simulator in *Airplane Mode*.</span></span> <span data-ttu-id="d43dc-130">Cela crée un scénario hors connexion.</span><span class="sxs-lookup"><span data-stu-id="d43dc-130">This creates an offline scenario.</span></span>
2. <span data-ttu-id="d43dc-131">Ajoutez des *tâches* , ou marquez-en certaines comme terminées.</span><span class="sxs-lookup"><span data-stu-id="d43dc-131">Add some *ToDo* items, or mark some items as complete.</span></span> <span data-ttu-id="d43dc-132">Quittez l’appareil ou le simulateur (ou forcez la fermeture de l’application) et redémarrez.</span><span class="sxs-lookup"><span data-stu-id="d43dc-132">Quit the device or simulator (or forcibly close the app) and restart.</span></span> <span data-ttu-id="d43dc-133">Vérifiez que vos modifications persistent sur l’appareil, car elles sont stockées dans le magasin SQLite local.</span><span class="sxs-lookup"><span data-stu-id="d43dc-133">Verify that your changes have been persisted on the device because they are held in the local SQLite store.</span></span>
3. <span data-ttu-id="d43dc-134">Affichez le contenu de la table *TodoItem* d’Azure avec un outil SQL, par exemple *SQL Server Management Studio* ou un client REST, comme *Fiddler* ou *Postman*.</span><span class="sxs-lookup"><span data-stu-id="d43dc-134">View the contents of the Azure *TodoItem* table either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span> <span data-ttu-id="d43dc-135">Vérifiez que les nouveaux éléments n’ont *pas* été synchronisés avec le serveur</span><span class="sxs-lookup"><span data-stu-id="d43dc-135">Verify that the new items have *not* been synced to the server</span></span>
   
       + <span data-ttu-id="d43dc-136">Pour un backend Node.js, accédez au [portail Azure](https://portal.azure.com/), puis dans votre backend d’application mobile, cliquez sur **Tables faciles** > **TodoItem** pour afficher le contenu de la table `TodoItem`.</span><span class="sxs-lookup"><span data-stu-id="d43dc-136">For a Node.js backend, go to the [Azure portal](https://portal.azure.com/), and in your Mobile App backend click **Easy Tables** > **TodoItem** to view the contents of the `TodoItem` table.</span></span>
       + <span data-ttu-id="d43dc-137">Pour un backend .NET, affichez le contenu de la table avec un outil SQL, par exemple *SQL Server Management Studio* ou un client REST, comme *Fiddler* ou *Postman*.</span><span class="sxs-lookup"><span data-stu-id="d43dc-137">For a .NET backend, view the table contents either with a SQL tool such as *SQL Server Management Studio*, or a REST client such as *Fiddler* or *Postman*.</span></span>
4. <span data-ttu-id="d43dc-138">Activez le Wi-Fi sur le simulateur ou l’appareil.</span><span class="sxs-lookup"><span data-stu-id="d43dc-138">Turn on WiFi in the device or simulator.</span></span> <span data-ttu-id="d43dc-139">Appuyez ensuite sur le bouton **Actualiser** .</span><span class="sxs-lookup"><span data-stu-id="d43dc-139">Next, press the **Refresh** button.</span></span>
5. <span data-ttu-id="d43dc-140">Affichez à nouveau les données TodoItem sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d43dc-140">View the TodoItem data again in the Azure portal.</span></span> <span data-ttu-id="d43dc-141">Les nouveaux éléments TodoItems et ceux modifiés doivent maintenant s'afficher.</span><span class="sxs-lookup"><span data-stu-id="d43dc-141">The new and changed TodoItems should now appear.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d43dc-142">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="d43dc-142">Additional Resources</span></span>
* <span data-ttu-id="d43dc-143">[Synchronisation des données hors connexion dans Azure Mobile Apps]</span><span class="sxs-lookup"><span data-stu-id="d43dc-143">[Offline Data Sync in Azure Mobile Apps]</span></span>
* <span data-ttu-id="d43dc-144">[Cloud Cover : synchronisation hors connexion dans Azure Mobile Services] \(remarque : le contexte de la vidéo est Mobile Services, mais la synchronisation hors connexion fonctionne de la même manière dans Azure Mobile Apps\)</span><span class="sxs-lookup"><span data-stu-id="d43dc-144">[Cloud Cover: Offline Sync in Azure Mobile Services] \(note: the video is on Mobile Services, but offline sync works in a similar way in Azure Mobile Apps\)</span></span>

<!-- URLs. -->

<span data-ttu-id="d43dc-145">[Synchronisation des données hors connexion dans Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span><span class="sxs-lookup"><span data-stu-id="d43dc-145">[Offline Data Sync in Azure Mobile Apps]: app-service-mobile-offline-data-sync.md</span></span>

<span data-ttu-id="d43dc-146">[Création d’une application Android]: app-service-mobile-android-get-started.md</span><span class="sxs-lookup"><span data-stu-id="d43dc-146">[Create an Android App]: app-service-mobile-android-get-started.md</span></span>

<span data-ttu-id="d43dc-147">[Cloud Cover : synchronisation hors connexion dans Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span><span class="sxs-lookup"><span data-stu-id="d43dc-147">[Cloud Cover: Offline Sync in Azure Mobile Services]: http://channel9.msdn.com/Shows/Cloud+Cover/Episode-155-Offline-Storage-with-Donna-Malayeri</span></span>
[Azure Friday: Offline-enabled apps in Azure Mobile Services]: http://azure.microsoft.com/documentation/videos/azure-mobile-services-offline-enabled-apps-with-donna-malayeri/

