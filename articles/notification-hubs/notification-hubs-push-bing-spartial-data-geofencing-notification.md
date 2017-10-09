---
title: "notifications push d’aaaGeo-balisés avec Azure Notification Hubs et des données spatiales Bing | Documents Microsoft"
description: "Dans ce didacticiel, vous allez apprendre comment toodeliver basée sur l’emplacement push notifications avec Azure Notification Hubs et des données spatiales Bing."
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
ms.openlocfilehash: d6efe473537f2159240c53e780741f12619c045d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a><span data-ttu-id="c285b-104">Notifications push avec clôture virtuelle avec Azure Notification Hubs et données spatiales Bing</span><span class="sxs-lookup"><span data-stu-id="c285b-104">Geo-fenced push notifications with Azure Notification Hubs and Bing Spatial Data</span></span>
> [!NOTE]
> <span data-ttu-id="c285b-105">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="c285b-105">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="c285b-106">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c285b-106">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c285b-107">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span><span class="sxs-lookup"><span data-stu-id="c285b-107">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).</span></span>
> 
> 

<span data-ttu-id="c285b-108">Dans ce didacticiel, vous allez apprendre comment toodeliver basée sur l’emplacement push notifications avec Azure Notification Hubs et des données spatiales Bing, exploitée à partir d’une application de plateforme Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="c285b-108">In this tutorial, you will learn how toodeliver location-based push notifications with Azure Notification Hubs and Bing Spatial Data, leveraged from within a Universal Windows Platform application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c285b-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c285b-109">Prerequisites</span></span>
<span data-ttu-id="c285b-110">Tout d’abord, vous devez toomake que vous avez tous les hello logiciels et services préalables :</span><span class="sxs-lookup"><span data-stu-id="c285b-110">First and foremost, you need toomake sure that you have all hello software and service pre-requisites:</span></span>

* <span data-ttu-id="c285b-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) ou ultérieur ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) convient également).</span><span class="sxs-lookup"><span data-stu-id="c285b-111">[Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) or later ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) will do as well).</span></span> 
* <span data-ttu-id="c285b-112">Version la plus récente de hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c285b-112">Latest version of hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> 
* <span data-ttu-id="c285b-113">[Compte Centre de développement Bing Cartes](https://www.bingmapsportal.com/) (vous pouvez en créer un gratuitement et l’associer à votre compte Microsoft).</span><span class="sxs-lookup"><span data-stu-id="c285b-113">[Bing Maps Dev Center account](https://www.bingmapsportal.com/) (you can create one for free and associate it with your Microsoft account).</span></span> 

## <a name="getting-started"></a><span data-ttu-id="c285b-114">Mise en route</span><span class="sxs-lookup"><span data-stu-id="c285b-114">Getting Started</span></span>
<span data-ttu-id="c285b-115">Commençons par créer le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-115">Let’s start by creating hello project.</span></span> <span data-ttu-id="c285b-116">Dans Visual Studio, démarrez un nouveau projet de type **Application vide (application Windows universelle)**.</span><span class="sxs-lookup"><span data-stu-id="c285b-116">In Visual Studio, start a new project of type **Blank App (Universal Windows)**.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

<span data-ttu-id="c285b-117">Une fois la création du projet hello est terminée, vous devez avoir atelier hello pour l’application hello lui-même.</span><span class="sxs-lookup"><span data-stu-id="c285b-117">Once hello project creation is complete, you should have hello harness for hello app itself.</span></span> <span data-ttu-id="c285b-118">Maintenant nous allons définir tous les éléments d’infrastructure de délimitation géographique hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-118">Now let’s set up everything for hello geo-fencing infrastructure.</span></span> <span data-ttu-id="c285b-119">Étant donné que nous toouse continue que des services Bing pour cela, il existe un point de terminaison REST API publique qui nous permet des frames tooquery emplacement spécifique :</span><span class="sxs-lookup"><span data-stu-id="c285b-119">Because we are going toouse Bing services for this, there is a public REST API endpoint that allows us tooquery specific location frames:</span></span>

    http://spatial.virtualearth.net/REST/v1/data/

<span data-ttu-id="c285b-120">Vous devez toospecify hello suivant tooget de paramètres qu’il fonctionne :</span><span class="sxs-lookup"><span data-stu-id="c285b-120">You will need toospecify hello following parameters tooget it working:</span></span>

* <span data-ttu-id="c285b-121">**ID de source de données** et **nom de source de données** : dans l’API Bing Cartes, les sources de données contiennent diverses métadonnées compartimentées, telles que les emplacements et les heures d’ouverture de l’opération.</span><span class="sxs-lookup"><span data-stu-id="c285b-121">**Data Source ID** and **Data Source Name** – in Bing Maps API, data sources contain various bucketed metadata, such as locations and business hours of operation.</span></span> <span data-ttu-id="c285b-122">Poursuivez la lecture pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="c285b-122">You can read more about those here.</span></span> 
* <span data-ttu-id="c285b-123">**Nom de l’entité** – hello entité toouse comme point de référence pour la notification de hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-123">**Entity Name** – hello entity you want toouse as a reference point for hello notification.</span></span> 
* <span data-ttu-id="c285b-124">**Clé de l’API Bing Maps** – il s’agit hello clé que vous avez obtenu précédemment lorsque vous avez créé le compte du centre de développement Bing hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-124">**Bing Maps API Key** – this is hello key that you obtained earlier when you created hello Bing Dev Center account.</span></span>

<span data-ttu-id="c285b-125">Nous allons suivre une présentation détaillée sur le programme d’installation hello pour chacun des éléments hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="c285b-125">Let’s do a deep-dive on hello setup for each of hello elements above.</span></span>

## <a name="setting-up-hello-data-source"></a><span data-ttu-id="c285b-126">Configuration de source de données hello</span><span class="sxs-lookup"><span data-stu-id="c285b-126">Setting up hello data source</span></span>
<span data-ttu-id="c285b-127">Vous pouvez le faire dans hello centre de développement de Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="c285b-127">You can do it in hello Bing Maps Dev Center.</span></span> <span data-ttu-id="c285b-128">Cliquez simplement sur **des sources de données** dans hello supérieur barre de navigation et sélectionnez **gérer les Sources de données**.</span><span class="sxs-lookup"><span data-stu-id="c285b-128">Simply click on **Data sources** in hello top navigation bar and select **Manage Data Sources**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

<span data-ttu-id="c285b-129">Si vous n’avez pas travaillé avec l’API Bing Maps avant, il ne sera pas agira probablement toutes les sources de données présentes, vous pouvez de créer un nouveau en cliquant sur la source de données tooa téléchargement.</span><span class="sxs-lookup"><span data-stu-id="c285b-129">If you have not worked with Bing Maps API before, most likely there won’t be any data sources present, so you can just create a new one by clicking on Upload data tooa data source.</span></span> <span data-ttu-id="c285b-130">Vérifiez que vous remplissez tous les champs hello requis :</span><span class="sxs-lookup"><span data-stu-id="c285b-130">Make sure you fill out all hello required fields:</span></span>

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

<span data-ttu-id="c285b-131">Vous vous demandez peut-être : quel est le fichier de données hello et ce qui devez vous être téléchargement ?</span><span class="sxs-lookup"><span data-stu-id="c285b-131">You might be wondering – what is hello data file and what should you be uploading?</span></span> <span data-ttu-id="c285b-132">Pour des raisons de hello de ce test, vous pouvez utiliser simplement l’exemple hello basée sur un canal qui encadre une zone de gens de San Francisco hello :</span><span class="sxs-lookup"><span data-stu-id="c285b-132">For hello purposes of this test, we can just use hello sample pipe-based that frames an area of hello San Francisco waterfront:</span></span>

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

<span data-ttu-id="c285b-133">Hello ci-dessus représente cette entité :</span><span class="sxs-lookup"><span data-stu-id="c285b-133">hello above represents this entity:</span></span>

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

<span data-ttu-id="c285b-134">Copiez et collez la chaîne hello ci-dessus dans un nouveau fichier et enregistrez-le sous simplement **NotificationHubsGeofence.pipe**et le télécharger dans hello centre de développement Bing.</span><span class="sxs-lookup"><span data-stu-id="c285b-134">Simply copy and paste hello string above into a new file and save it as **NotificationHubsGeofence.pipe**, and upload it in hello Bing Dev Center.</span></span>

> [!NOTE]
> <span data-ttu-id="c285b-135">Vous pouvez être invité à toospecify une nouvelle clé pour hello **clé principale** qui est différente de hello **clé de requête**.</span><span class="sxs-lookup"><span data-stu-id="c285b-135">You might be prompted toospecify a new key for hello **Master Key** that is different from hello **Query Key**.</span></span> <span data-ttu-id="c285b-136">Créez simplement une nouvelle clé via hello du tableau de bord et l’actualisation hello page source de données téléchargement.</span><span class="sxs-lookup"><span data-stu-id="c285b-136">Simply create a new key through hello dashboard and refresh hello data source upload page.</span></span>
> 
> 

<span data-ttu-id="c285b-137">Une fois que vous téléchargez le fichier de données hello, vous devez toomake, assurez-vous que vous publiez des sources de données hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-137">Once you upload hello data file, you will need toomake sure that you publish hello data source.</span></span> 

<span data-ttu-id="c285b-138">Accédez trop**gérer les Sources de données**, comme nous l’avons fait ci-dessus, recherchez votre source de données dans la liste de hello et cliquez sur **publier** Bonjour **Actions** colonne.</span><span class="sxs-lookup"><span data-stu-id="c285b-138">Go too**Manage Data Sources**, just like we did above, find your data source in hello list and click on **Publish** in hello **Actions** column.</span></span> <span data-ttu-id="c285b-139">Dans, vous devez voir votre source de données Bonjour **des Sources de données publiées** onglet :</span><span class="sxs-lookup"><span data-stu-id="c285b-139">In a bit, you should see your data source in hello **Published Data Sources** tab:</span></span>

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

<span data-ttu-id="c285b-140">Si vous cliquez sur **modifier**, vous sera en mesure de toosee un coup de œil les emplacements que nous avons présenté qu’il contient :</span><span class="sxs-lookup"><span data-stu-id="c285b-140">If you click **Edit**, you will be able toosee at a glance what locations we introduced in it:</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

<span data-ttu-id="c285b-141">À ce stade, le portail de hello n’affiche pas hello de limites pour geofence hello que nous avons créé – nous suffit d’une confirmation hello spécifié se trouve à proximité de droite hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-141">At this point, hello portal does not show you hello boundaries for hello geofence that we created – all we need is a confirmation that hello location specified is in hello right vicinity.</span></span>

<span data-ttu-id="c285b-142">Vous disposez maintenant de toutes les exigences de hello pour la source de données hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-142">Now you have all hello requirements for hello data source.</span></span> <span data-ttu-id="c285b-143">tooget hello plus d’informations sur les URL de demande hello d’appel d’API de hello Bonjour Bing Maps Dev Center, cliquez sur **des sources de données** et sélectionnez **les informations de Source de données**.</span><span class="sxs-lookup"><span data-stu-id="c285b-143">tooget hello details on hello request URL for hello API call, in hello Bing Maps Dev Center, click **Data sources** and select **Data Source Information**.</span></span>

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

<span data-ttu-id="c285b-144">Hello **URL de la requête** est ce que nous sommes après ici.</span><span class="sxs-lookup"><span data-stu-id="c285b-144">hello **Query URL** is what we’re after here.</span></span> <span data-ttu-id="c285b-145">Il s’agit de point de terminaison hello par rapport à laquelle nous pouvons exécuter des requêtes toocheck si hello appareil est actuellement dans les limites de hello d’un emplacement ou non.</span><span class="sxs-lookup"><span data-stu-id="c285b-145">This is hello endpoint against which we can execute queries toocheck whether hello device is currently within hello boundaries of a location or not.</span></span> <span data-ttu-id="c285b-146">tooperform cette vérification, il suffit de tooexecute GET appeler par rapport à l’URL de la requête hello, avec hello ajoutés des paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="c285b-146">tooperform this check, we simply need tooexecute a GET call against hello query URL, with hello following parameters appended:</span></span>

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

<span data-ttu-id="c285b-147">De cette façon, vous indiquez un point cible que nous obtenons à partir de l’appareil de hello et Bing Maps effectue automatiquement hello calculs toosee si elle se trouve dans hello geofence.</span><span class="sxs-lookup"><span data-stu-id="c285b-147">That way you're specifying a target point that we obtain from hello device and Bing Maps will automatically perform hello calculations toosee whether it is within hello geofence.</span></span> <span data-ttu-id="c285b-148">Une fois que vous exécutez la requête hello via un navigateur (ou cURL), vous obtiendrez standard une réponse JSON :</span><span class="sxs-lookup"><span data-stu-id="c285b-148">Once you execute hello request through a browser (or cURL), you will get standard a JSON response:</span></span>

![](./media/notification-hubs-geofence/bing-maps-json.png)

<span data-ttu-id="c285b-149">Cette réponse se produit uniquement lorsque le point de hello est réellement dans hello désigné des limites.</span><span class="sxs-lookup"><span data-stu-id="c285b-149">This response only happens when hello point is actually within hello designated boundaries.</span></span> <span data-ttu-id="c285b-150">Si ce n’est pas le cas, vous obtiendrez un compartiment **results** vide :</span><span class="sxs-lookup"><span data-stu-id="c285b-150">If it is not, you will get an empty **results** bucket:</span></span>

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a><span data-ttu-id="c285b-151">Configuration d’application de plateforme Windows universelle hello</span><span class="sxs-lookup"><span data-stu-id="c285b-151">Setting up hello UWP application</span></span>
<span data-ttu-id="c285b-152">Maintenant que nous avons la source de données hello prêt, nous pouvons commencer à travailler sur hello application UWP qui nous amorcés précédemment.</span><span class="sxs-lookup"><span data-stu-id="c285b-152">Now that we have hello data source ready, we can start working on hello UWP application that we bootstrapped earlier.</span></span>

<span data-ttu-id="c285b-153">Tout d’abord, nous devons activer les services de localisation pour l’application.</span><span class="sxs-lookup"><span data-stu-id="c285b-153">First and foremost, we must enable location services for our application.</span></span> <span data-ttu-id="c285b-154">toodo, double-cliquez sur `Package.appxmanifest` fichier **l’Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="c285b-154">toodo this, double-click on `Package.appxmanifest` file in **Solution Explorer**.</span></span>

![](./media/notification-hubs-geofence/vs-package-manifest.png)

<span data-ttu-id="c285b-155">Dans l’onglet de propriétés du package hello que vous venez d’ouvrir, cliquez sur **fonctionnalités** et assurez-vous que vous sélectionnez **emplacement**:</span><span class="sxs-lookup"><span data-stu-id="c285b-155">In hello package properties tab that just opened, click on **Capabilities** and make sure that you select **Location**:</span></span>

![](./media/notification-hubs-geofence/vs-package-location.png)

<span data-ttu-id="c285b-156">Capacité d’emplacement hello est déclarée, créez un nouveau dossier dans votre solution nommée `Core`et ajoutez un nouveau fichier au sein de celui-ci, appelée `LocationHelper.cs`:</span><span class="sxs-lookup"><span data-stu-id="c285b-156">As hello location capability is declared, create a new folder in your solution named `Core`, and add a new file within it, called `LocationHelper.cs`:</span></span>

![](./media/notification-hubs-geofence/vs-location-helper.png)

<span data-ttu-id="c285b-157">Hello `LocationHelper` classe proprement dite est relativement simple à ce stade, il ne nous permet emplacement de l’utilisateur tooobtain hello via les API du système hello :</span><span class="sxs-lookup"><span data-stu-id="c285b-157">hello `LocationHelper` class itself is fairly basic at this point – all it does is allow us tooobtain hello user location through hello system API:</span></span>

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

<span data-ttu-id="c285b-158">Vous pouvez en savoir plus sur l’obtention hello d’emplacement de l’utilisateur dans les applications UWP officiel de hello [document MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span><span class="sxs-lookup"><span data-stu-id="c285b-158">You can read more about getting hello user’s location in UWP apps in hello official [MSDN document](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).</span></span>

<span data-ttu-id="c285b-159">toocheck acquisition d’emplacement hello fonctionne, ouvrez le côté de code hello de votre page d’accueil (`MainPage.xaml.cs`).</span><span class="sxs-lookup"><span data-stu-id="c285b-159">toocheck that hello location acquisition is actually working, open hello code side of your main page (`MainPage.xaml.cs`).</span></span> <span data-ttu-id="c285b-160">Créer un nouveau gestionnaire d’événements hello `Loaded` événement Bonjour `MainPage` constructeur :</span><span class="sxs-lookup"><span data-stu-id="c285b-160">Create a new event handler for hello `Loaded` event in hello `MainPage` constructor:</span></span>

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

<span data-ttu-id="c285b-161">implémentation de Hello hello du Gestionnaire d’événements est la suivante :</span><span class="sxs-lookup"><span data-stu-id="c285b-161">hello implementation of hello event handler is as follows:</span></span>

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

<span data-ttu-id="c285b-162">Notez que nous déclarée Gestionnaire de hello asynchrones, car `GetCurrentLocation` est await et par conséquent requiert toobe exécutée dans un contexte asynchrone.</span><span class="sxs-lookup"><span data-stu-id="c285b-162">Notice that we declared hello handler as async because `GetCurrentLocation` is awaitable, and therefore requires toobe executed in an async context.</span></span> <span data-ttu-id="c285b-163">En outre, étant donné que dans certaines circonstances, nous pouvons se retrouver avec un emplacement null (par exemple, les services d’emplacement hello sont désactivés ou application hello a été refusée l’emplacement de tooaccess autorisations), nous devons toomake assurer qu’elle est gérée correctement avec une vérification de valeur null.</span><span class="sxs-lookup"><span data-stu-id="c285b-163">Also, because under certain circumstances we might end up with a null location (e.g. hello location services are disabled or hello application was denied permissions tooaccess location), we need toomake sure that it is properly handled with a null check.</span></span>

<span data-ttu-id="c285b-164">Exécutez l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-164">Run hello application.</span></span> <span data-ttu-id="c285b-165">Assurez-vous d’avoir autorisé l’accès à l’emplacement :</span><span class="sxs-lookup"><span data-stu-id="c285b-165">Make sure you allow location access:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

<span data-ttu-id="c285b-166">Une fois hello lancements d’applications, vous devez être en mesure de toosee hello coordonnées hello **sortie** fenêtre :</span><span class="sxs-lookup"><span data-stu-id="c285b-166">Once hello application launches, you should be able toosee hello coordinates in hello **Output** window:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

<span data-ttu-id="c285b-167">Maintenant, vous savez qu’emplacement acquisition works – vous pouvez Gestionnaire d’événements tooremove libre hello test pour chargé, car nous ne l’utilise pas plus.</span><span class="sxs-lookup"><span data-stu-id="c285b-167">Now you know that location acquisition works – feel free tooremove hello test event handler for Loaded because we won’t be using it anymore.</span></span>

<span data-ttu-id="c285b-168">étape suivante de Hello est toocapture changements d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="c285b-168">hello next step is toocapture location changes.</span></span> <span data-ttu-id="c285b-169">Pour ce faire, passons arrière toohello `LocationHelper` classe et ajoutez le Gestionnaire d’événements hello pour `PositionChanged`:</span><span class="sxs-lookup"><span data-stu-id="c285b-169">For that, let’s go back toohello `LocationHelper` class and add hello event handler for `PositionChanged`:</span></span>

    geolocator.PositionChanged += Geolocator_PositionChanged;

<span data-ttu-id="c285b-170">implémentation de Hello affichera des coordonnées d’emplacement hello Bonjour **sortie** fenêtre :</span><span class="sxs-lookup"><span data-stu-id="c285b-170">hello implementation will show hello location coordinates in hello **Output** window:</span></span>

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a><span data-ttu-id="c285b-171">Configuration de serveur principal de hello</span><span class="sxs-lookup"><span data-stu-id="c285b-171">Setting up hello backend</span></span>
<span data-ttu-id="c285b-172">Télécharger hello [exemple de serveur principal .NET à partir de GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="c285b-172">Download hello [.NET Backend Sample from GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> <span data-ttu-id="c285b-173">Une fois que hello téléchargement terminé, ouvrez hello `NotifyUsers` dossier et par la suite : hello `NotifyUsers.sln` fichier.</span><span class="sxs-lookup"><span data-stu-id="c285b-173">Once hello download completes, open hello `NotifyUsers` folder, and subsequently – hello `NotifyUsers.sln` file.</span></span>

<span data-ttu-id="c285b-174">Ensemble hello `AppBackend` projet comme hello **projet de démarrage** et lancez-le.</span><span class="sxs-lookup"><span data-stu-id="c285b-174">Set hello `AppBackend` project as hello **StartUp Project** and launch it.</span></span>

![](./media/notification-hubs-geofence/vs-startup-project.png)

<span data-ttu-id="c285b-175">Hello projet est déjà configuré toosend push notifications tootarget pour les appareils, donc nous devrons toodo limitent – permuter la chaîne de connexion adéquate hello hello hub de notification et ajouter une limite d’identification toosend hello notification uniquement lorsque hello se trouve dans hello geofence.</span><span class="sxs-lookup"><span data-stu-id="c285b-175">hello project is already configured toosend push notifications tootarget devices, so we’ll need toodo only two things – swap out hello right connection string for hello notification hub and add boundary identification toosend hello notification only when hello user is within hello geofence.</span></span>

<span data-ttu-id="c285b-176">chaîne de connexion tooconfigure hello, Bonjour `Models` dossier ouvert `Notifications.cs`.</span><span class="sxs-lookup"><span data-stu-id="c285b-176">tooconfigure hello connection string, in hello `Models` folder open `Notifications.cs`.</span></span> <span data-ttu-id="c285b-177">Hello `NotificationHubClient.CreateClientFromConnectionString` la fonction doit contenir hello plus d’informations sur votre concentrateur de notification que vous pouvez obtenir Bonjour [portail Azure](https://portal.azure.com) (Rechercher à l’intérieur de hello **des stratégies d’accès** lame  **Paramètres**).</span><span class="sxs-lookup"><span data-stu-id="c285b-177">hello `NotificationHubClient.CreateClientFromConnectionString` function should contain hello information about your notification hub that you can get in hello [Azure Portal](https://portal.azure.com) (look inside hello **Access Policies** blade in **Settings**).</span></span> <span data-ttu-id="c285b-178">Enregistrez le fichier de configuration mis à jour hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-178">Save hello updated configuration file.</span></span>

<span data-ttu-id="c285b-179">Nous devons maintenant toocreate un modèle pour hello résultat de l’API Bing Maps.</span><span class="sxs-lookup"><span data-stu-id="c285b-179">Now we need toocreate a model for hello Bing Maps API result.</span></span> <span data-ttu-id="c285b-180">Hello toodo de façon plus simple qui est avec le bouton droit sur hello `Models` dossier, **ajouter** > **classe**.</span><span class="sxs-lookup"><span data-stu-id="c285b-180">hello easiest way toodo that is right-click on hello `Models` folder, **Add** > **Class**.</span></span> <span data-ttu-id="c285b-181">Nommez-le `GeofenceBoundary.cs`.</span><span class="sxs-lookup"><span data-stu-id="c285b-181">Name it `GeofenceBoundary.cs`.</span></span> <span data-ttu-id="c285b-182">Après cela, copiez hello JSON à partir de la réponse hello API dont nous avons parlé dans la première section de hello et en cours d’utilisation de Visual Studio **modifier** > **Collage spécial** > **coller JSON en tant que Classes**.</span><span class="sxs-lookup"><span data-stu-id="c285b-182">Once done, copy hello JSON from hello API response that we discussed in hello first section and in Visual Studio use **Edit** > **Paste Special** > **Paste JSON as Classes**.</span></span> 

<span data-ttu-id="c285b-183">De cette façon, nous nous assurons que cet objet hello est désérialisée exactement telle qu’elle a été conçu.</span><span class="sxs-lookup"><span data-stu-id="c285b-183">That way we ensure that hello object will be deserialized exactly as it was intended.</span></span> <span data-ttu-id="c285b-184">La classe obtenue doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="c285b-184">Your resulting class set should resemble this:</span></span>

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

<span data-ttu-id="c285b-185">Ensuite, ouvrez `Controllers` > `NotificationsController.cs`.</span><span class="sxs-lookup"><span data-stu-id="c285b-185">Next, open `Controllers` > `NotificationsController.cs`.</span></span> <span data-ttu-id="c285b-186">Nous devons tootweak hello Post appel tooaccount de latitude et longitude de cible hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-186">We need tootweak hello Post call tooaccount for hello target longitude and latitude.</span></span> <span data-ttu-id="c285b-187">Pour ce faire, ajoutez simplement signature de fonction deux chaînes toohello – `latitude` et `longitude`.</span><span class="sxs-lookup"><span data-stu-id="c285b-187">For that, simply add two strings toohello function signature – `latitude` and `longitude`.</span></span>

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

<span data-ttu-id="c285b-188">Créez une classe dans le projet hello appelé `ApiHelper.cs` – nous allons l’utiliser intersections de tooconnect tooBing toocheck point limite.</span><span class="sxs-lookup"><span data-stu-id="c285b-188">Create a new class within hello project called `ApiHelper.cs` – we’ll use it tooconnect tooBing toocheck point boundary intersections.</span></span> <span data-ttu-id="c285b-189">Implémentez une fonction `IsPointWithinBounds` de la manière suivante :</span><span class="sxs-lookup"><span data-stu-id="c285b-189">Implement a `IsPointWithinBounds` function, like this:</span></span>

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
> <span data-ttu-id="c285b-190">Assurez-vous que toosubstitute hello API de point de terminaison avec hello URL de la requête que vous avez obtenu précédemment de hello centre de développement Bing (même règle s’applique toohello API clé).</span><span class="sxs-lookup"><span data-stu-id="c285b-190">Make sure toosubstitute hello API endpoint with hello query URL that you obtained earlier from hello Bing Dev Center (same applies toohello API key).</span></span> 
> 
> 

<span data-ttu-id="c285b-191">S’il existe des requêtes toohello de résultats, cela signifie que hello point spécifié se trouve dans les limites de hello de hello geofence, donc nous revenons `true`.</span><span class="sxs-lookup"><span data-stu-id="c285b-191">If there are results toohello query, that means that hello specified point is within hello boundaries of hello geofence, so we return `true`.</span></span> <span data-ttu-id="c285b-192">S’il n’y a aucun résultat, Bing nous indique que le point de hello est en dehors de la frame de recherche hello, donc nous revenons `false`.</span><span class="sxs-lookup"><span data-stu-id="c285b-192">If there are no results, Bing is telling us that hello point is outside hello lookup frame, so we return `false`.</span></span>

<span data-ttu-id="c285b-193">Dans `NotificationsController.cs`, créer une vérification juste avant l’instruction switch hello :</span><span class="sxs-lookup"><span data-stu-id="c285b-193">Back in `NotificationsController.cs`, create a check right before hello switch statement:</span></span>

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

<span data-ttu-id="c285b-194">De cette façon, les notifications hello sont envoyée uniquement lorsque le point de hello se trouve dans les limites de hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-194">That way, hello notification is only sent when hello point is within hello boundaries.</span></span>

## <a name="testing-push-notifications-in-hello-uwp-app"></a><span data-ttu-id="c285b-195">Test des notifications push dans l’application de plateforme Windows universelle hello</span><span class="sxs-lookup"><span data-stu-id="c285b-195">Testing push notifications in hello UWP app</span></span>
<span data-ttu-id="c285b-196">Si vous revenez en application de plateforme Windows universelle toohello, nous devons maintenant être tootest en mesure de notifications.</span><span class="sxs-lookup"><span data-stu-id="c285b-196">Going back toohello UWP app, we should now be able tootest notifications.</span></span> <span data-ttu-id="c285b-197">Au sein de hello `LocationHelper` de classe, créez une fonction – `SendLocationToBackend`:</span><span class="sxs-lookup"><span data-stu-id="c285b-197">Within hello `LocationHelper` class, create a new function – `SendLocationToBackend`:</span></span>

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
> <span data-ttu-id="c285b-198">Échange hello `POST_URL` emplacement toohello de votre application web déployés que vous avez créée dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-198">Swap hello `POST_URL` toohello location of your deployed web application that we created in hello previous section.</span></span> <span data-ttu-id="c285b-199">Pour l’instant, il est OK toorun localement, mais lorsque vous travaillez sur le déploiement d’une version publique, vous devrez toohost avec un fournisseur externe.</span><span class="sxs-lookup"><span data-stu-id="c285b-199">For now, it’s OK toorun it locally, but as you work on deploying a public version, you will need toohost it with an external provider.</span></span>
> 
> 

<span data-ttu-id="c285b-200">Nous allons maintenant vous assurer que nous enregistrons application UWP de hello pour les notifications push.</span><span class="sxs-lookup"><span data-stu-id="c285b-200">Let’s now make sure that we register hello UWP app for push notifications.</span></span> <span data-ttu-id="c285b-201">Dans Visual Studio, cliquez sur **projet** > **stocker** > **associer application hello store**.</span><span class="sxs-lookup"><span data-stu-id="c285b-201">In Visual Studio, click on **Project** > **Store** > **Associate app with hello store**.</span></span>

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

<span data-ttu-id="c285b-202">Une fois que vous vous connectez dans le compte de développeur tooyour, assurez-vous que vous sélectionnez une application existante ou créez un nouveau et lui associez les package hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-202">Once you sign in tooyour developer account, make sure you select an existing app or create a new one and associate hello package with it.</span></span> 

<span data-ttu-id="c285b-203">Accédez centre de développement toohello et application hello ouverts que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="c285b-203">Go toohello Dev Center and open hello app that you just created.</span></span> <span data-ttu-id="c285b-204">Cliquez sur **Services** > **Notifications push** > **Services Microsoft Live**.</span><span class="sxs-lookup"><span data-stu-id="c285b-204">Click **Services** > **Push Notifications** > **Live Services site**.</span></span>

![](./media/notification-hubs-geofence/ms-live-services.png)

<span data-ttu-id="c285b-205">Sur le site de hello, prenez note de hello **Secret d’Application** et hello **SID du Package**.</span><span class="sxs-lookup"><span data-stu-id="c285b-205">On hello site, take note of hello **Application Secret** and hello **Package SID**.</span></span> <span data-ttu-id="c285b-206">Vous devez à la fois dans hello portail Azure, ouvrez votre concentrateur de notification, cliquez sur **paramètres** > **Notification Services** > **Windows (WNS)**et entrez les informations de hello dans les champs hello requis.</span><span class="sxs-lookup"><span data-stu-id="c285b-206">You will need both in hello Azure Portal – open your notification hub, click on **Settings** > **Notification Services** > **Windows (WNS)** and enter hello information in hello required fields.</span></span>

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

<span data-ttu-id="c285b-207">Cliquez sur **Save**(Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="c285b-207">Click on **Save**.</span></span>

<span data-ttu-id="c285b-208">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Références**, puis sélectionnez **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c285b-208">Right click on **References** in **Solution Explorer** and select **Manage NuGet Packages**.</span></span> <span data-ttu-id="c285b-209">Nous devons tooadd un toohello référence **bibliothèque managée de Microsoft Azure Service Bus** – simplement rechercher `WindowsAzure.Messaging.Managed` et ajoutez-le tooyour projet.</span><span class="sxs-lookup"><span data-stu-id="c285b-209">We will need tooadd a reference toohello **Microsoft Azure Service Bus managed library** – simply search for `WindowsAzure.Messaging.Managed` and add it tooyour project.</span></span>

![](./media/notification-hubs-geofence/vs-nuget.png)

<span data-ttu-id="c285b-210">À des fins de test, nous pouvons créer hello `MainPage_Loaded` Gestionnaire d’événements une fois encore et ajoutez cette tooit d’extrait de code :</span><span class="sxs-lookup"><span data-stu-id="c285b-210">For testing purposes, we can create hello `MainPage_Loaded` event handler once again, and add this code snippet tooit:</span></span>

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

<span data-ttu-id="c285b-211">Hello ci-dessus inscrit application hello avec concentrateur de notification hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-211">hello above registers hello app with hello notification hub.</span></span> <span data-ttu-id="c285b-212">Vous êtes prêt toogo !</span><span class="sxs-lookup"><span data-stu-id="c285b-212">You are ready toogo!</span></span> 

<span data-ttu-id="c285b-213">Dans `LocationHelper`, à l’intérieur de hello `Geolocator_PositionChanged` gestionnaire, vous pouvez ajouter un élément de code de test qui force place emplacement hello hello geofence :</span><span class="sxs-lookup"><span data-stu-id="c285b-213">In `LocationHelper`, inside hello `Geolocator_PositionChanged` handler, you can add a piece of test code that will forcefully put hello location inside hello geofence:</span></span>

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

<span data-ttu-id="c285b-214">Étant donné que nous ne réussissent pas les coordonnées réel hello (qui peuvent être dans les limites de hello moment hello) et que vous utilisez des valeurs de test prédéfinies, nous allons voir une notification s’affichent sur la mise à jour :</span><span class="sxs-lookup"><span data-stu-id="c285b-214">Because we are not passing hello real coordinates (which might not be within hello boundaries at hello moment) and are using predefined test values, we will see a notification show up on update:</span></span>

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a><span data-ttu-id="c285b-215">Et ensuite ?</span><span class="sxs-lookup"><span data-stu-id="c285b-215">What’s next?</span></span>
<span data-ttu-id="c285b-216">Il existe quelques étapes que vous devrez peut-être toofollow dans toohello Ajout ci-dessus toomake assurer que les solutions hello sont prêt pour la production.</span><span class="sxs-lookup"><span data-stu-id="c285b-216">There are a couple of steps that you might need toofollow in addition toohello above toomake sure that hello solution is production-ready.</span></span>

<span data-ttu-id="c285b-217">Tout d’abord, vous devrez peut-être tooensure que geofences sont dynamiques.</span><span class="sxs-lookup"><span data-stu-id="c285b-217">First and foremost, you might need tooensure that geofences are dynamic.</span></span> <span data-ttu-id="c285b-218">Cette opération nécessite du travail supplémentaire avec hello API Bing dans l’ordre toobe tooupload en mesure de nouveau des limites au sein de la source de données existante hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-218">This will require some extra work with hello Bing API in order toobe able tooupload new boundaries within hello existing data source.</span></span> <span data-ttu-id="c285b-219">Consultez hello [documentation de l’API de Services de données spatiales Bing](https://msdn.microsoft.com/library/ff701734.aspx) pour plus d’informations sur le sujet de hello.</span><span class="sxs-lookup"><span data-stu-id="c285b-219">Consult hello [Bing Spatial Data Services API documentation](https://msdn.microsoft.com/library/ff701734.aspx) for more details on hello subject.</span></span>

<span data-ttu-id="c285b-220">En second lieu, comme vous tooensure de travail que la remise de hello est effectuée toohello des participants à droite, vous souhaiterez peut-être tootarget leur via [marquage](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="c285b-220">Second, as you are working tooensure that hello delivery is done toohello right participants, you might want tootarget them via [tagging](notification-hubs-tags-segment-push-message.md).</span></span>

<span data-ttu-id="c285b-221">solution Hello ci-dessus décrit un scénario dans lequel vous pourrez avoir un large éventail de plateformes cibles, afin que nous ne pas limiter hello géorepérage toosystem fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="c285b-221">hello solution shown above describes a scenario in which you might have a wide variety of target platforms, so we did not limit hello geofencing toosystem-specific capabilities.</span></span> <span data-ttu-id="c285b-222">Ceci dit, hello plateforme Windows universelle offre des fonctions trop[détecter geofences droite out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span><span class="sxs-lookup"><span data-stu-id="c285b-222">That said, hello Universal Windows Platform offers capabilities too[detect geofences right out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).</span></span>

<span data-ttu-id="c285b-223">Pour plus de détails concernant les fonctionnalités de Notification Hubs, consultez le [portail documentaire](https://azure.microsoft.com/documentation/services/notification-hubs/).</span><span class="sxs-lookup"><span data-stu-id="c285b-223">For more details regarding Notification Hubs capabilities, check out our [documentation portal](https://azure.microsoft.com/documentation/services/notification-hubs/).</span></span>

