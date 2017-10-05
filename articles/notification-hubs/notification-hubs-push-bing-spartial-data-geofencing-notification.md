---
title: "Notifications push avec clôture virtuelle avec Azure Notification Hubs et données spatiales Bing | Microsoft Docs"
description: "Ce didacticiel vous présente comment envoyer des notifications push en fonction du lieu avec Azure Notification Hubs et les données spatiales Bing."
services: notification-hubs
documentationcenter: windows
keywords: notification push, notification push
author: dend
manager: yuaxu
editor: dend
ms.assetid: f41beea1-0d62-4418-9ffc-c9d70607a1b7
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/31/2016
ms.author: dendeli
ms.openlocfilehash: b2a84e0479aac9ded08bb64e1ea20ddee6636cce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="c5174-104">Notifications push avec clôture virtuelle avec Azure Notification Hubs et données spatiales Bing</span><span class="sxs-lookup"><span data-stu-id="c5174-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="c5174-105">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="c5174-105">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="c5174-106">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c5174-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c5174-107">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span><span class="sxs-lookup"><span data-stu-id="c5174-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="c5174-108">Ce didacticiel vous présente comment envoyer des notifications push en fonction du lieu avec Azure Notification Hubs et des données spatiales Bing, exploitées à partir d’une application de plateforme Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="c5174-108">In this tutorial, you will learn how to deliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5174-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c5174-109">Prerequisites</span></span>
<span data-ttu-id="c5174-110">Tout d’abord, assurez-vous de disposer de tous les logiciels et services requis :</span><span class="sxs-lookup"><span data-stu-id="c5174-110">First and foremost, you need to make sure that you have all the software and service pre-requisites:</span></span>

* <span data-ttu-id="c5174-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) ou ultérieur ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) convient également).</span><span class="sxs-lookup"><span data-stu-id="c5174-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="c5174-112">[Kit de développement logiciel (SDK) Azure](https://azure.microsoft.com/downloads/)dans sa version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="c5174-112">Latest version of the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="c5174-113">[Compte Centre de développement Bing Cartes](https://www.bingmapsportal.com/) (vous pouvez en créer un gratuitement et l’associer à votre compte Microsoft).</span><span class="sxs-lookup"><span data-stu-id="c5174-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="c5174-114">Mise en route</span><span class="sxs-lookup"><span data-stu-id="c5174-114">Getting Started</span></span>
<span data-ttu-id="c5174-115">Commençons par créer le projet.</span><span class="sxs-lookup"><span data-stu-id="c5174-115">Let’s start by creating the project.</span></span> <span data-ttu-id="c5174-116">Dans Visual Studio, démarrez un nouveau projet de type **Application vide (application Windows universelle)**.</span><span class="sxs-lookup"><span data-stu-id="c5174-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="c5174-117">Une fois le projet créé, vous pouvez commencer à exploiter l’application.</span><span class="sxs-lookup"><span data-stu-id="c5174-117">Once the project creation is complete, you should have the harness for the app itself.</span></span> <span data-ttu-id="c5174-118">Nous allons à présent définir l’infrastructure de clôture virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c5174-118">Now let’s set up everything for the geo-fencing infrastructure.</span></span> <span data-ttu-id="c5174-119">Pour ce faire, nous allons utiliser les services Bing ; nous pouvons ainsi interroger des infrastructures de localisation spécifiques grâce à un point de terminaison d’API REST public :</span><span class="sxs-lookup"><span data-stu-id="c5174-119">Because we are going to use Bing services for this, there is a public REST API endpoint that allows us to query specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="c5174-120">Pour que cela fonctionne, vous devez spécifier les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="c5174-120">You will need to specify the following parameters to get it working:</span></span>

* <span data-ttu-id="c5174-121">**ID de source de données** et **nom de source de données** : dans l’API Bing Cartes, les sources de données contiennent diverses métadonnées compartimentées, telles que les emplacements et les heures d’ouverture de l’opération.</span><span class="sxs-lookup"><span data-stu-id="c5174-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="c5174-122">Poursuivez la lecture pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="c5174-122">You can read more about those here.</span></span> 
* <span data-ttu-id="c5174-123">**Nom d’entité** : l’entité que vous souhaitez utiliser comme point de référence pour la notification.</span><span class="sxs-lookup"><span data-stu-id="c5174-123">**Entity Name** – the entity you want to use as a reference point for the notification.</span></span> 
* <span data-ttu-id="c5174-124">**Clé d’API Bing Cartes** : il s’agit de la clé que vous avez obtenue précédemment lorsque vous avez créé le compte Centre de développement Bing.</span><span class="sxs-lookup"><span data-stu-id="c5174-124">**Bing Maps API Key** – this is the key that you obtained earlier when you created the Bing Dev Center account.</span></span>

<span data-ttu-id="c5174-125">Passons en revue la configuration de chacun des éléments ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="c5174-125">Let’s do a deep-dive on the setup for each of the elements above.</span></span>

## <a name="setting-up-the-data-source"></a><span data-ttu-id="c5174-126">Configuration de la source de données</span><span class="sxs-lookup"><span data-stu-id="c5174-126">Setting up the data source</span></span>
<span data-ttu-id="c5174-127">Celle-ci peut être faite dans le Centre de développement Bing Cartes.</span><span class="sxs-lookup"><span data-stu-id="c5174-127">You can do it in the Bing Maps Dev Center.</span></span> <span data-ttu-id="c5174-128">Cliquez simplement sur **Sources de données** dans la barre de navigation supérieure, puis sélectionnez **Gérer les sources de données**.</span><span class="sxs-lookup"><span data-stu-id="c5174-128">Simply click on **Data sources** in the top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="c5174-129">Si vous n’avez jamais travaillé avec l’API Bing Cartes, celle-ci ne présentera probablement pas de sources de données. Cliquez sur Télécharger des données vers une source de données pour créer une source de données.</span><span class="sxs-lookup"><span data-stu-id="c5174-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data to a data source.</span></span> <span data-ttu-id="c5174-130">Assurez-vous de remplir tous les champs obligatoires :</span><span class="sxs-lookup"><span data-stu-id="c5174-130">Make sure you fill out all the required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="c5174-131">Vous vous demandez peut-être ce qu’est le fichier de données et ce que vous devez télécharger.</span><span class="sxs-lookup"><span data-stu-id="c5174-131">You might be wondering – what is the data file and what should you be uploading?</span></span> <span data-ttu-id="c5174-132">Dans le cadre de ce test, nous pouvons simplement utiliser l’exemple au format pipe qui encadre une partie des quais de San Francisco :</span><span class="sxs-lookup"><span data-stu-id="c5174-132">For the purposes of this test, we can just use the sample pipe-based that frames an area of the San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="c5174-133">Cette chaîne représente l’entité suivante :</span><span class="sxs-lookup"><span data-stu-id="c5174-133">The above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="c5174-134">Copiez et collez la chaîne ci-dessus dans un nouveau fichier et enregistrez-le sous le nom **NotificationHubsGeofence.pipe**, puis téléchargez-le dans le Centre de développement Bing.</span><span class="sxs-lookup"><span data-stu-id="c5174-134">Simply copy and paste the string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in the Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="c5174-135">Vous serez peut-être invité à spécifier une nouvelle clé pour la **clé principale** qui diffère de la **clé de requête**.</span><span class="sxs-lookup"><span data-stu-id="c5174-135">You might be prompted to specify a new key for the **Master Key** that is different from the **Query Key**.</span></span> <span data-ttu-id="c5174-136">Créez simplement une clé dans le tableau de bord et actualisez la page de téléchargement de la source de données.</span><span class="sxs-lookup"><span data-stu-id="c5174-136">Simply create a new key through the dashboard and refresh the data source upload page.</span></span>
> 
> 

<span data-ttu-id="c5174-137">Une fois que vous avez téléchargé le fichier de données, vous devez publier la source de données.</span><span class="sxs-lookup"><span data-stu-id="c5174-137">Once you upload the data file, you will need to make sure that you publish the data source.</span></span> 

<span data-ttu-id="c5174-138">Accédez à **Gérer les sources de données** (comme vu précédemment), recherchez la source de données dans la liste, puis cliquez sur **Publier** dans la colonne **Actions**.</span><span class="sxs-lookup"><span data-stu-id="c5174-138">Go to **Manage Data Sources**, just like we did above, find your data source in the list and click on **Publish** in the **Actions** column.</span></span> <span data-ttu-id="c5174-139">Vous verrez votre source de données dans l’onglet **Sources de données publiées** d’ici quelques instants :</span><span class="sxs-lookup"><span data-stu-id="c5174-139">In a bit, you should see your data source in the **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="c5174-140">Si vous cliquez sur **Modifier**, vous verrez rapidement quels emplacements nous avons introduits dans celle-ci :</span><span class="sxs-lookup"><span data-stu-id="c5174-140">If you click **Edit**, you will be able to see at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="c5174-141">À ce stade, le portail n’indique pas les limites de la clôture virtuelle que nous avons créée. Nous devons seulement avoir la confirmation que l’emplacement spécifié se trouve dans la bonne zone.</span><span class="sxs-lookup"><span data-stu-id="c5174-141">At this point, the portal does not show you the boundaries for the geofence that we created – all we need is a confirmation that the location specified is in the right vicinity.</span></span>

<span data-ttu-id="c5174-142">Toutes les conditions nécessaires sont désormais remplies pour la source de données.</span><span class="sxs-lookup"><span data-stu-id="c5174-142">Now you have all the requirements for the data source.</span></span> <span data-ttu-id="c5174-143">Pour obtenir plus d’informations sur l’URL de la demande pour l’appel d’API, cliquez sur **Sources de données** dans le Centre de développement Bing Cartes, puis sélectionnez **Informations sur la source de données**.</span><span class="sxs-lookup"><span data-stu-id="c5174-143">To get the details on the request URL for the API call, in the Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="c5174-144">C’est l’ **URL de requête** qui nous intéresse à présent.</span><span class="sxs-lookup"><span data-stu-id="c5174-144">The **Query URL** is what we’re after here.</span></span> <span data-ttu-id="c5174-145">C’est le point de terminaison sur lequel nous pouvons exécuter des requêtes pour vérifier si l’appareil se trouve dans les limites d’un emplacement ou non.</span><span class="sxs-lookup"><span data-stu-id="c5174-145">This is the endpoint against which we can execute queries to check whether the device is currently within the boundaries of a location or not.</span></span> <span data-ttu-id="c5174-146">Pour effectuer cette vérification, il suffit d’exécuter un appel GET sur l’URL de requête, en ajoutant les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="c5174-146">To perform this check, we simply need to execute a GET call against the query URL, with the following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="c5174-147">De cette façon, vous spécifiez un point cible que nous obtenons grâce à l’appareil, et Bing Cartes calcule automatiquement si celui-ci se trouve dans les limites de la clôture virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c5174-147">That way you're specifying a target point that we obtain from the device and Bing Maps will automatically perform the calculations to see whether it is within the geofence.</span></span> <span data-ttu-id="c5174-148">Lorsque vous exécutez la requête via un navigateur (ou cURL), vous obtenez une réponse JSON standard :</span><span class="sxs-lookup"><span data-stu-id="c5174-148">Once you execute the request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="c5174-149">Cette réponse se produit uniquement lorsque le point se trouve bien dans les limites désignées.</span><span class="sxs-lookup"><span data-stu-id="c5174-149">This response only happens when the point is actually within the designated boundaries.</span></span> <span data-ttu-id="c5174-150">Si ce n’est pas le cas, vous obtiendrez un compartiment **results** vide :</span><span class="sxs-lookup"><span data-stu-id="c5174-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-the-uwp-application"></a><span data-ttu-id="c5174-151">Configuration de l’application UWP</span><span class="sxs-lookup"><span data-stu-id="c5174-151">Setting up the UWP application</span></span>
<span data-ttu-id="c5174-152">Maintenant que la source de données est prête, nous pouvons commencer à travailler sur l’application UWP commencée précédemment.</span><span class="sxs-lookup"><span data-stu-id="c5174-152">Now that we have the data source ready, we can start working on the UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="c5174-153">Tout d’abord, nous devons activer les services de localisation pour l’application.</span><span class="sxs-lookup"><span data-stu-id="c5174-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="c5174-154">Pour ce faire, double-cliquez sur le fichier `Package.appxmanifest` dans l’ **Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="c5174-154">To do this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="c5174-155">Dans l’onglet de propriétés du package que vous venez d’ouvrir, cliquez sur **Capacités**, puis sélectionnez **Localisation** :</span><span class="sxs-lookup"><span data-stu-id="c5174-155">In the package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="c5174-156">Après avoir déclaré la fonctionnalité de localisation, créez un dossier dans votre solution appelé `Core`, puis créez un fichier appelé `LocationHelper.cs` dans ce dernier :</span><span class="sxs-lookup"><span data-stu-id="c5174-156">As the location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="c5174-157">La classe `LocationHelper` est assez basique à ce stade ; elle permet uniquement d’obtenir l’emplacement de l’utilisateur via l’API système :</span><span class="sxs-lookup"><span data-stu-id="c5174-157">The `LocationHelper` class itself is fairly basic at this point – all it does is allow us to obtain the user location through the system API:</span></span>

    using System;
    using System.Threading.Tasks;
    using Windows.Devices.Geolocation;

    namespace NotificationHubs.Geofence.Core
    {
        public class LocationHelper
        {
            private static readonly uint AppDesiredAccuracyInMeters = 10;

            public async static Task<Geoposition> GetCurrentLocation()
            {
                var accessStatus = await Geolocator.RequestAccessAsync();
                switch (accessStatus)
                {
                    case GeolocationAccessStatus.Allowed:
                        {
                            Geolocator geolocator = new Geolocator { DesiredAccuracyInMeters = AppDesiredAccuracyInMeters };

                            return await geolocator.GetGeopositionAsync();
                        }
                    default:
                        {
                            return null;
                        }
                }
            }

        }
    }

<span data-ttu-id="c5174-158">Pour en savoir plus sur l’obtention de l’emplacement de l’utilisateur dans les applications UWP, consultez le [document MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx)officiel.</span><span class="sxs-lookup"><span data-stu-id="c5174-158">You can read more about getting the user’s location in UWP apps in the official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="c5174-159">Pour vérifier que l’obtention de l’emplacement fonctionne correctement, accédez au code de votre page d’accueil (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="c5174-159">To check that the location acquisition is actually working, open the code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="c5174-160">Créez un gestionnaire d’événements pour l’événement `Loaded` dans le constructeur `MainPage` :</span><span class="sxs-lookup"><span data-stu-id="c5174-160">Create a new event handler for the `Loaded` event in the `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="c5174-161">L’implémentation du gestionnaire d’événements se fait de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="c5174-161">The implementation of the event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="c5174-162">Notez que nous avons déclaré le gestionnaire asynchrone, car `GetCurrentLocation` peut être attendu et doit donc être exécuté dans un contexte asynchrone.</span><span class="sxs-lookup"><span data-stu-id="c5174-162">Notice that we declared the handler as async because `GetCurrentLocation` is awaitable, and therefore requires to be executed in an async context.</span></span> <span data-ttu-id="c5174-163">En outre, un emplacement Null peut se présenter dans certains cas (par exemple lorsque les services de localisation sont désactivés ou lorsque l’application n’est pas autorisée à accéder à l’emplacement). Cela impose un traitement par validation de valeur Null.</span><span class="sxs-lookup"><span data-stu-id="c5174-163">Also, because under certain circumstances we might end up with a null location (e.g. the location services are disabled or the application was denied permissions to access location), we need to make sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="c5174-164">Exécutez l'application.</span><span class="sxs-lookup"><span data-stu-id="c5174-164">Run the application.</span></span> <span data-ttu-id="c5174-165">Assurez-vous d’avoir autorisé l’accès à l’emplacement :</span><span class="sxs-lookup"><span data-stu-id="c5174-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="c5174-166">Lorsque l’application démarre, vous devez être en mesure de voir les coordonnées dans la fenêtre **Sortie** :</span><span class="sxs-lookup"><span data-stu-id="c5174-166">Once the application launches, you should be able to see the coordinates in the **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="c5174-167">Vous savez désormais que l’obtention de l’emplacement fonctionne ; n’hésitez pas à supprimer le gestionnaire d’événements de test pour Loaded, car vous ne l’utiliserez plus.</span><span class="sxs-lookup"><span data-stu-id="c5174-167">Now you know that location acquisition works – feel free to remove the test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="c5174-168">L’étape suivante consiste à capturer le changement d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="c5174-168">The next step is to capture location changes.</span></span> <span data-ttu-id="c5174-169">Pour ce faire, revenez à la classe `LocationHelper` et ajoutez le gestionnaire d’événements pour `PositionChanged` :</span><span class="sxs-lookup"><span data-stu-id="c5174-169">For that, let’s go back to the `LocationHelper` class and add the event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="c5174-170">L’implémentation affichera les coordonnées de l’emplacement dans la fenêtre **Sortie** :</span><span class="sxs-lookup"><span data-stu-id="c5174-170">The implementation will show the location coordinates in the **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-the-backend"></a><span data-ttu-id="c5174-171">Configuration du backend</span><span class="sxs-lookup"><span data-stu-id="c5174-171">Setting up the backend</span></span>
<span data-ttu-id="c5174-172">Téléchargez [l’exemple de backend .NET sur GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="c5174-172">Download the [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="c5174-173">Une fois téléchargé, ouvrez le dossier `NotifyUsers`, puis le fichier `NotifyUsers.sln`.</span><span class="sxs-lookup"><span data-stu-id="c5174-173">Once the download completes, open the `NotifyUsers` folder, and subsequently – the `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="c5174-174">Définissez le projet `AppBackend` comme **Projet de démarrage** , puis exécutez-le.</span><span class="sxs-lookup"><span data-stu-id="c5174-174">Set the `AppBackend` project as the **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="c5174-175">Le projet est déjà configuré pour envoyer des notifications push aux appareils cibles. Vous aurez seulement deux actions à effectuer : permuter la bonne chaîne de connexion pour le hub de notification et ajouter l’identification des limites afin d’envoyer une notification uniquement lorsque l’utilisateur se trouve dans les limites de la clôture virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c5174-175">The project is already configured to send push notifications to target devices, so we’ll need to do only two things – swap out the right connection string for the notification hub and add boundary identification to send the notification only when the user is within the geofence.</span></span>

<span data-ttu-id="c5174-176">Pour configurer la chaîne de connexion dans le dossier `Models`, ouvrez `Notifications.cs`.</span><span class="sxs-lookup"><span data-stu-id="c5174-176">To configure the connection string, in the `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="c5174-177">La fonction `NotificationHubClient.CreateClientFromConnectionString` doit contenir les informations sur votre hub de notification que vous pouvez obtenir dans le [portail Azure](https://portal.azure.com) (consultez le panneau **Stratégies d’accès** dans **Paramètres**).</span><span class="sxs-lookup"><span data-stu-id="c5174-177">The `NotificationHubClient.CreateClientFromConnectionString` function should contain the information about your notification hub that you can get in the [Azure Portal](https://portal.azure.com) (look inside the **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="c5174-178">Enregistrez le fichier de configuration mis à jour.</span><span class="sxs-lookup"><span data-stu-id="c5174-178">Save the updated configuration file.</span></span>

<span data-ttu-id="c5174-179">Vous devez à présent créer un modèle pour le résultat de l’API Bing Cartes.</span><span class="sxs-lookup"><span data-stu-id="c5174-179">Now we need to create a model for the Bing Maps API result.</span></span> <span data-ttu-id="c5174-180">Pour ce faire, la méthode la plus simple consiste à cliquer avec le bouton droit sur le dossier `Models`, puis à cliquer sur **Ajouter** > **Classe**.</span><span class="sxs-lookup"><span data-stu-id="c5174-180">The easiest way to do that is right-click on the `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="c5174-181">Nommez-le `GeofenceBoundary.cs`.</span><span class="sxs-lookup"><span data-stu-id="c5174-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="c5174-182">Une fois cette opération effectuée, copiez le code JSON de la réponse d’API vu dans la première section. Dans Visual Studio, cliquez sur **Modifier** > **Collage spécial** > **Coller le code JSON en tant que classes**.</span><span class="sxs-lookup"><span data-stu-id="c5174-182">Once done, copy the JSON from the API response that we discussed in the first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="c5174-183">De cette façon, l’objet sera désérialisé (ce qui était l’objectif).</span><span class="sxs-lookup"><span data-stu-id="c5174-183">That way we ensure that the object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="c5174-184">La classe obtenue doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="c5174-184">Your resulting class set should resemble this:</span></span>

    namespace AppBackend.Models
    {
        public class Rootobject
        {
            public D d { get; set; }
        }

        public class D
        {
            public string __copyright { get; set; }
            public Result[] results { get; set; }
        }

        public class Result
        {
            public __Metadata __metadata { get; set; }
            public string EntityID { get; set; }
            public string Name { get; set; }
            public float Longitude { get; set; }
            public float Latitude { get; set; }
            public string Boundary { get; set; }
            public string Confidence { get; set; }
            public string Locality { get; set; }
            public string AddressLine { get; set; }
            public string AdminDistrict { get; set; }
            public string CountryRegion { get; set; }
            public string PostalCode { get; set; }
        }

        public class __Metadata
        {
            public string uri { get; set; }
        }
    }

<span data-ttu-id="c5174-185">Ensuite, ouvrez `Controllers` > `NotificationsController.cs`.</span><span class="sxs-lookup"><span data-stu-id="c5174-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="c5174-186">L’appel POST doit être modifié afin de prendre en compte la longitude et la latitude cibles.</span><span class="sxs-lookup"><span data-stu-id="c5174-186">We need to tweak the Post call to account for the target longitude and latitude.</span></span> <span data-ttu-id="c5174-187">Pour cela, ajoutez simplement deux chaînes à la signature de la fonction : `latitude` et `longitude`.</span><span class="sxs-lookup"><span data-stu-id="c5174-187">For that, simply add two strings to the function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="c5174-188">Créez une classe dans le projet appelée `ApiHelper.cs`. Celle-ci permet de se connecter à Bing afin de vérifier les intersections des limites des points.</span><span class="sxs-lookup"><span data-stu-id="c5174-188">Create a new class within the project called `ApiHelper.cs` – we’ll use it to connect to Bing to check point boundary intersections.</span></span> <span data-ttu-id="c5174-189">Implémentez une fonction `IsPointWithinBounds` de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="c5174-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

    public class ApiHelper
    {
        public static readonly string ApiEndpoint = "{YOUR_QUERY_ENDPOINT}?spatialFilter=intersects(%27POINT%20({0}%20{1})%27)&$format=json&key={2}";
        public static readonly string ApiKey = "{YOUR_API_KEY}";

        public static bool IsPointWithinBounds(string longitude,string latitude)
        {
            var json = new WebClient().DownloadString(string.Format(ApiEndpoint, longitude, latitude, ApiKey));
            var result = JsonConvert.DeserializeObject<Rootobject>(json);
            if (result.d.results != null && result.d.results.Count() > 0)
            {
                return true;
            }
            else
            {
                return false;
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="c5174-190">Veillez à remplacer le point de terminaison d’API avec l’URL de requête obtenue précédemment dans le Centre de développement Bing (cela s’applique également à la clé d’API).</span><span class="sxs-lookup"><span data-stu-id="c5174-190">Make sure to substitute the API endpoint with the query URL that you obtained earlier from the Bing Dev Center (same applies to the API key).</span></span> 
> 
> 

<span data-ttu-id="c5174-191">Si la requête renvoie des résultats, cela signifie que le point spécifié se trouve dans les limites de la clôture virtuelle. Vous devez donc retourner `true`.</span><span class="sxs-lookup"><span data-stu-id="c5174-191">If there are results to the query, that means that the specified point is within the boundaries of the geofence, so we return `true`.</span></span> <span data-ttu-id="c5174-192">Si Bing ne renvoie pas de résultats, cela signifie que le point se trouve en dehors des limites de la recherche. Vous devez donc retourner `false`.</span><span class="sxs-lookup"><span data-stu-id="c5174-192">If there are no results, Bing is telling us that the point is outside the lookup frame, so we return `false`.</span></span>

<span data-ttu-id="c5174-193">Dans `NotificationsController.cs`, créez une vérification juste avant l’instruction switch :</span><span class="sxs-lookup"><span data-stu-id="c5174-193">Back in `NotificationsController.cs`, create a check right before the switch statement:</span></span>

    if (ApiHelper.IsPointWithinBounds(longitude, latitude))
    {
        switch (pns.ToLower())
        {
            case "wns":
                //// Windows 8.1 / Windows Phone 8.1
                var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                // Windows 10 specific Action Center support
                toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
                            "From " + user + ": " + message + "</text></binding></visual></toast>";
                outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

                break;
        }
    }

<span data-ttu-id="c5174-194">De cette façon, la notification est envoyée uniquement lorsque le point se trouve dans les limites.</span><span class="sxs-lookup"><span data-stu-id="c5174-194">That way, the notification is only sent when the point is within the boundaries.</span></span>

## <a name="testing-push-notifications-in-the-uwp-app"></a><span data-ttu-id="c5174-195">Test des notifications push dans l’application UWP</span><span class="sxs-lookup"><span data-stu-id="c5174-195">Testing push notifications in the UWP app</span></span>
<span data-ttu-id="c5174-196">Concernant l’application UWP, vous devriez à présent être en mesure de tester les notifications.</span><span class="sxs-lookup"><span data-stu-id="c5174-196">Going back to the UWP app, we should now be able to test notifications.</span></span> <span data-ttu-id="c5174-197">Dans la classe `LocationHelper`, créez une fonction `SendLocationToBackend` :</span><span class="sxs-lookup"><span data-stu-id="c5174-197">Within the `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

    public static async Task SendLocationToBackend(string pns, string userTag, string message, string latitude, string longitude)
    {
        var POST_URL = "http://localhost:8741/api/notifications?pns=" +
            pns + "&to_tag=" + userTag + "&latitude=" + latitude + "&longitude=" + longitude;

        using (var httpClient = new HttpClient())
        {
            try
            {
                await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                    System.Text.Encoding.UTF8, "application/json"));
            }
            catch (Exception ex)
            {
                Debug.WriteLine(ex.Message);
            }
        }
    }

> [!NOTE]
> <span data-ttu-id="c5174-198">Permutez `POST_URL` à l’emplacement de votre application web déployée que vous avez créée à la section précédente.</span><span class="sxs-lookup"><span data-stu-id="c5174-198">Swap the `POST_URL` to the location of your deployed web application that we created in the previous section.</span></span> <span data-ttu-id="c5174-199">Il est possible de l’exécuter localement pour le moment, mais lorsque vous travaillez sur le déploiement d’une version publique, vous devrez l’héberger avec un fournisseur externe.</span><span class="sxs-lookup"><span data-stu-id="c5174-199">For now, it’s OK to run it locally, but as you work on deploying a public version, you will need to host it with an external provider.</span></span>
> 
> 

<span data-ttu-id="c5174-200">Assurez-vous d’inscrire l’application UWP pour les notifications push.</span><span class="sxs-lookup"><span data-stu-id="c5174-200">Let’s now make sure that we register the UWP app for push notifications.</span></span> <span data-ttu-id="c5174-201">Dans Visual Studio, cliquez sur **Projet** > **Store** > **Associer l’application au Windows Store**.</span><span class="sxs-lookup"><span data-stu-id="c5174-201">In Visual Studio, click on **Project** > **Store** > **Associate app with the store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="c5174-202">Une fois que vous êtes connecté à votre compte de développeur, sélectionnez une application existante ou créez une application et associez le package à celle-ci.</span><span class="sxs-lookup"><span data-stu-id="c5174-202">Once you sign in to your developer account, make sure you select an existing app or create a new one and associate the package with it.</span></span> 

<span data-ttu-id="c5174-203">Accédez au Centre de développement et ouvrez l’application que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="c5174-203">Go to the Dev Center and open the app that you just created.</span></span> <span data-ttu-id="c5174-204">Cliquez sur **Services** > **Notifications push** > **Services Microsoft Live**.</span><span class="sxs-lookup"><span data-stu-id="c5174-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="c5174-205">Sur le site, prenez note du **Secret d’application** et du **Package SID**.</span><span class="sxs-lookup"><span data-stu-id="c5174-205">On the site, take note of the **Application Secret** and the **Package SID**.</span></span> <span data-ttu-id="c5174-206">Vous aurez besoin de ces deux éléments dans le portail Azure. Ouvrez votre hub de notification, cliquez sur **Paramètres** > **Services de notification** > **Windows (WNS)** et entrez les informations dans les champs requis.</span><span class="sxs-lookup"><span data-stu-id="c5174-206">You will need both in the Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter the information in the required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="c5174-207">Cliquez sur **Save**(Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="c5174-207">Click on **Save**.</span></span>

<span data-ttu-id="c5174-208">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Références**, puis sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c5174-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="c5174-209">Vous devrez ajouter une référence à la **bibliothèque managée Microsoft Azure Service Bus** ; recherchez simplement `WindowsAzure.Messaging.Managed` et ajoutez-le à votre projet.</span><span class="sxs-lookup"><span data-stu-id="c5174-209">We will need to add a reference to the **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it to your project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="c5174-210">À des fins de test, vous pouvez recréer le gestionnaire d’événements `MainPage_Loaded` , puis lui ajouter cet extrait de code :</span><span class="sxs-lookup"><span data-stu-id="c5174-210">For testing purposes, we can create the `MainPage_Loaded` event handler once again, and add this code snippet to it:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays the registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="c5174-211">Le code ci-dessus inscrit l’application auprès du hub de notification.</span><span class="sxs-lookup"><span data-stu-id="c5174-211">The above registers the app with the notification hub.</span></span> <span data-ttu-id="c5174-212">Vous avez terminé !</span><span class="sxs-lookup"><span data-stu-id="c5174-212">You are ready to go!</span></span> 

<span data-ttu-id="c5174-213">Dans `LocationHelper`, à l’intérieur du gestionnaire `Geolocator_PositionChanged`, vous pouvez ajouter un extrait de code de test qui force l’emplacement à l’intérieur des limites de la clôture virtuelle :</span><span class="sxs-lookup"><span data-stu-id="c5174-213">In `LocationHelper`, inside the `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put the location inside the geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="c5174-214">Étant donné que vous ne transmettez pas les coordonnées réelles (qui ne se trouvent peut-être pas dans les limites actuellement) et que vous utilisez des valeurs de test prédéfinies, vous verrez une notification s’afficher lors de la mise à jour :</span><span class="sxs-lookup"><span data-stu-id="c5174-214">Because we are not passing the real coordinates (which might not be within the boundaries at the moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="c5174-215">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="c5174-215">What’s next?</span></span>
<span data-ttu-id="c5174-216">Vous devrez peut-être suivre quelques étapes supplémentaires outre celles présentées ci-dessus pour vous assurer que la solution est prête pour la production.</span><span class="sxs-lookup"><span data-stu-id="c5174-216">There are a couple of steps that you might need to follow in addition to the above to make sure that the solution is production-ready.</span></span>

<span data-ttu-id="c5174-217">Tout d’abord, assurez-vous que la clôture virtuelle est dynamique.</span><span class="sxs-lookup"><span data-stu-id="c5174-217">First and foremost, you might need to ensure that geofences are dynamic.</span></span> <span data-ttu-id="c5174-218">Cette opération nécessite des actions supplémentaires avec l’API Bing pour pouvoir télécharger les nouvelles limites au sein de la source de données existante.</span><span class="sxs-lookup"><span data-stu-id="c5174-218">This will require some extra work with the Bing API in order to be able to upload new boundaries within the existing data source.</span></span> <span data-ttu-id="c5174-219">Pour plus d’informations sur ce sujet, consultez la [documentation de l’API de Services de données spatiales Bing](https://msdn.microsoft.com/library/ff701734.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c5174-219">Consult the [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on the subject.</span></span>

<span data-ttu-id="c5174-220">Ensuite, vous pouvez cibler les participants appropriés par [balisage](notification-hubs-tags-segment-push-message.md)pour garantir une remise correcte.</span><span class="sxs-lookup"><span data-stu-id="c5174-220">Second, as you are working to ensure that the delivery is done to the right participants, you might want to target them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="c5174-221">La solution ci-dessus décrit un scénario dans lequel vous disposez d’un large choix de plateformes cibles. La clôture virtuelle n’a donc pas été limitée à des fonctionnalités spécifiques du système.</span><span class="sxs-lookup"><span data-stu-id="c5174-221">The solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit the geofencing to system-specific capabilities.</span></span> <span data-ttu-id="c5174-222">Ceci dit, la plateforme Windows universelle offre des fonctionnalités [prêtes à l’emploi pouvant détecter les clôtures virtuelles](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="c5174-222">That said, the Universal Windows Platform offers capabilities to [detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="c5174-223">Pour plus de détails concernant les fonctionnalités de Notification Hubs, consultez le [portail documentaire](https://azure.microsoft.com/documentation/services/notification-hubs/).</span><span class="sxs-lookup"><span data-stu-id="c5174-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

