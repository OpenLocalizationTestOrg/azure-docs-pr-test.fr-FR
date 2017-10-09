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
# <a name="geo-fenced-push-notifications-with-azure-notification-hubs-and-bing-spatial-data"></a>Notifications push avec clôture virtuelle avec Azure Notification Hubs et données spatiales Bing
> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02).
> 
> 

Dans ce didacticiel, vous allez apprendre comment toodeliver basée sur l’emplacement push notifications avec Azure Notification Hubs et des données spatiales Bing, exploitée à partir d’une application de plateforme Windows universelle.

## <a name="prerequisites"></a>Composants requis
Tout d’abord, vous devez toomake que vous avez tous les hello logiciels et services préalables :

* [Visual Studio 2015 Update 1](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx) ou ultérieur ([Community Edition](https://go.microsoft.com/fwlink/?LinkId=691978&clcid=0x409) convient également). 
* Version la plus récente de hello [Azure SDK](https://azure.microsoft.com/downloads/). 
* [Compte Centre de développement Bing Cartes](https://www.bingmapsportal.com/) (vous pouvez en créer un gratuitement et l’associer à votre compte Microsoft). 

## <a name="getting-started"></a>Mise en route
Commençons par créer le projet de hello. Dans Visual Studio, démarrez un nouveau projet de type **Application vide (application Windows universelle)**.

![](./media/notification-hubs-geofence/notification-hubs-create-blank-app.png)

Une fois la création du projet hello est terminée, vous devez avoir atelier hello pour l’application hello lui-même. Maintenant nous allons définir tous les éléments d’infrastructure de délimitation géographique hello. Étant donné que nous toouse continue que des services Bing pour cela, il existe un point de terminaison REST API publique qui nous permet des frames tooquery emplacement spécifique :

    http://spatial.virtualearth.net/REST/v1/data/

Vous devez toospecify hello suivant tooget de paramètres qu’il fonctionne :

* **ID de source de données** et **nom de source de données** : dans l’API Bing Cartes, les sources de données contiennent diverses métadonnées compartimentées, telles que les emplacements et les heures d’ouverture de l’opération. Poursuivez la lecture pour en savoir plus. 
* **Nom de l’entité** – hello entité toouse comme point de référence pour la notification de hello. 
* **Clé de l’API Bing Maps** – il s’agit hello clé que vous avez obtenu précédemment lorsque vous avez créé le compte du centre de développement Bing hello.

Nous allons suivre une présentation détaillée sur le programme d’installation hello pour chacun des éléments hello ci-dessus.

## <a name="setting-up-hello-data-source"></a>Configuration de source de données hello
Vous pouvez le faire dans hello centre de développement de Bing Maps. Cliquez simplement sur **des sources de données** dans hello supérieur barre de navigation et sélectionnez **gérer les Sources de données**.

![](./media/notification-hubs-geofence/bing-maps-manage-data.png)

Si vous n’avez pas travaillé avec l’API Bing Maps avant, il ne sera pas agira probablement toutes les sources de données présentes, vous pouvez de créer un nouveau en cliquant sur la source de données tooa téléchargement. Vérifiez que vous remplissez tous les champs hello requis :

![](./media/notification-hubs-geofence/bing-maps-create-data.png)

Vous vous demandez peut-être : quel est le fichier de données hello et ce qui devez vous être téléchargement ? Pour des raisons de hello de ce test, vous pouvez utiliser simplement l’exemple hello basée sur un canal qui encadre une zone de gens de San Francisco hello :

    Bing Spatial Data Services, 1.0, TestBoundaries
    EntityID(Edm.String,primaryKey)|Name(Edm.String)|Longitude(Edm.Double)|Latitude(Edm.Double)|Boundary(Edm.Geography)
    1|SanFranciscoPier|||POLYGON ((-122.389825 37.776598,-122.389438 37.773087,-122.381885 37.771849,-122.382186 37.777022,-122.389825 37.776598))

Hello ci-dessus représente cette entité :

![](./media/notification-hubs-geofence/bing-maps-geofence.png)

Copiez et collez la chaîne hello ci-dessus dans un nouveau fichier et enregistrez-le sous simplement **NotificationHubsGeofence.pipe**et le télécharger dans hello centre de développement Bing.

> [!NOTE]
> Vous pouvez être invité à toospecify une nouvelle clé pour hello **clé principale** qui est différente de hello **clé de requête**. Créez simplement une nouvelle clé via hello du tableau de bord et l’actualisation hello page source de données téléchargement.
> 
> 

Une fois que vous téléchargez le fichier de données hello, vous devez toomake, assurez-vous que vous publiez des sources de données hello. 

Accédez trop**gérer les Sources de données**, comme nous l’avons fait ci-dessus, recherchez votre source de données dans la liste de hello et cliquez sur **publier** Bonjour **Actions** colonne. Dans, vous devez voir votre source de données Bonjour **des Sources de données publiées** onglet :

![](./media/notification-hubs-geofence/bing-maps-published-data.png)

Si vous cliquez sur **modifier**, vous sera en mesure de toosee un coup de œil les emplacements que nous avons présenté qu’il contient :

![](./media/notification-hubs-geofence/bing-maps-data-details.png)

À ce stade, le portail de hello n’affiche pas hello de limites pour geofence hello que nous avons créé – nous suffit d’une confirmation hello spécifié se trouve à proximité de droite hello.

Vous disposez maintenant de toutes les exigences de hello pour la source de données hello. tooget hello plus d’informations sur les URL de demande hello d’appel d’API de hello Bonjour Bing Maps Dev Center, cliquez sur **des sources de données** et sélectionnez **les informations de Source de données**.

![](./media/notification-hubs-geofence/bing-maps-data-info.png)

Hello **URL de la requête** est ce que nous sommes après ici. Il s’agit de point de terminaison hello par rapport à laquelle nous pouvons exécuter des requêtes toocheck si hello appareil est actuellement dans les limites de hello d’un emplacement ou non. tooperform cette vérification, il suffit de tooexecute GET appeler par rapport à l’URL de la requête hello, avec hello ajoutés des paramètres suivants :

    ?spatialFilter=intersects(%27POINT%20LONGITUDE%20LATITUDE)%27)&$format=json&key=QUERY_KEY

De cette façon, vous indiquez un point cible que nous obtenons à partir de l’appareil de hello et Bing Maps effectue automatiquement hello calculs toosee si elle se trouve dans hello geofence. Une fois que vous exécutez la requête hello via un navigateur (ou cURL), vous obtiendrez standard une réponse JSON :

![](./media/notification-hubs-geofence/bing-maps-json.png)

Cette réponse se produit uniquement lorsque le point de hello est réellement dans hello désigné des limites. Si ce n’est pas le cas, vous obtiendrez un compartiment **results** vide :

![](./media/notification-hubs-geofence/bing-maps-nores.png)

## <a name="setting-up-hello-uwp-application"></a>Configuration d’application de plateforme Windows universelle hello
Maintenant que nous avons la source de données hello prêt, nous pouvons commencer à travailler sur hello application UWP qui nous amorcés précédemment.

Tout d’abord, nous devons activer les services de localisation pour l’application. toodo, double-cliquez sur `Package.appxmanifest` fichier **l’Explorateur de solutions**.

![](./media/notification-hubs-geofence/vs-package-manifest.png)

Dans l’onglet de propriétés du package hello que vous venez d’ouvrir, cliquez sur **fonctionnalités** et assurez-vous que vous sélectionnez **emplacement**:

![](./media/notification-hubs-geofence/vs-package-location.png)

Capacité d’emplacement hello est déclarée, créez un nouveau dossier dans votre solution nommée `Core`et ajoutez un nouveau fichier au sein de celui-ci, appelée `LocationHelper.cs`:

![](./media/notification-hubs-geofence/vs-location-helper.png)

Hello `LocationHelper` classe proprement dite est relativement simple à ce stade, il ne nous permet emplacement de l’utilisateur tooobtain hello via les API du système hello :

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

Vous pouvez en savoir plus sur l’obtention hello d’emplacement de l’utilisateur dans les applications UWP officiel de hello [document MSDN](https://msdn.microsoft.com/library/windows/apps/mt219698.aspx).

toocheck acquisition d’emplacement hello fonctionne, ouvrez le côté de code hello de votre page d’accueil (`MainPage.xaml.cs`). Créer un nouveau gestionnaire d’événements hello `Loaded` événement Bonjour `MainPage` constructeur :

    public MainPage()
    {
        this.InitializeComponent();
        this.Loaded += MainPage_Loaded;
    }

implémentation de Hello hello du Gestionnaire d’événements est la suivante :

    private async void MainPage_Loaded(object sender, RoutedEventArgs e)
    {
        var location = await LocationHelper.GetCurrentLocation();

        if (location != null)
        {
            Debug.WriteLine(string.Concat(location.Coordinate.Longitude,
                " ", location.Coordinate.Latitude));
        }
    }

Notez que nous déclarée Gestionnaire de hello asynchrones, car `GetCurrentLocation` est await et par conséquent requiert toobe exécutée dans un contexte asynchrone. En outre, étant donné que dans certaines circonstances, nous pouvons se retrouver avec un emplacement null (par exemple, les services d’emplacement hello sont désactivés ou application hello a été refusée l’emplacement de tooaccess autorisations), nous devons toomake assurer qu’elle est gérée correctement avec une vérification de valeur null.

Exécutez l’application hello. Assurez-vous d’avoir autorisé l’accès à l’emplacement :

![](./media/notification-hubs-geofence/notification-hubs-location-access.png)

Une fois hello lancements d’applications, vous devez être en mesure de toosee hello coordonnées hello **sortie** fenêtre :

![](./media/notification-hubs-geofence/notification-hubs-location-output.png)

Maintenant, vous savez qu’emplacement acquisition works – vous pouvez Gestionnaire d’événements tooremove libre hello test pour chargé, car nous ne l’utilise pas plus.

étape suivante de Hello est toocapture changements d’emplacement. Pour ce faire, passons arrière toohello `LocationHelper` classe et ajoutez le Gestionnaire d’événements hello pour `PositionChanged`:

    geolocator.PositionChanged += Geolocator_PositionChanged;

implémentation de Hello affichera des coordonnées d’emplacement hello Bonjour **sortie** fenêtre :

    private static async void Geolocator_PositionChanged(Geolocator sender, PositionChangedEventArgs args)
    {
        await CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            Debug.WriteLine(string.Concat(args.Position.Coordinate.Longitude, " ", args.Position.Coordinate.Latitude));
        });
    }

## <a name="setting-up-hello-backend"></a>Configuration de serveur principal de hello
Télécharger hello [exemple de serveur principal .NET à partir de GitHub](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). Une fois que hello téléchargement terminé, ouvrez hello `NotifyUsers` dossier et par la suite : hello `NotifyUsers.sln` fichier.

Ensemble hello `AppBackend` projet comme hello **projet de démarrage** et lancez-le.

![](./media/notification-hubs-geofence/vs-startup-project.png)

Hello projet est déjà configuré toosend push notifications tootarget pour les appareils, donc nous devrons toodo limitent – permuter la chaîne de connexion adéquate hello hello hub de notification et ajouter une limite d’identification toosend hello notification uniquement lorsque hello se trouve dans hello geofence.

chaîne de connexion tooconfigure hello, Bonjour `Models` dossier ouvert `Notifications.cs`. Hello `NotificationHubClient.CreateClientFromConnectionString` la fonction doit contenir hello plus d’informations sur votre concentrateur de notification que vous pouvez obtenir Bonjour [portail Azure](https://portal.azure.com) (Rechercher à l’intérieur de hello **des stratégies d’accès** lame  **Paramètres**). Enregistrez le fichier de configuration mis à jour hello.

Nous devons maintenant toocreate un modèle pour hello résultat de l’API Bing Maps. Hello toodo de façon plus simple qui est avec le bouton droit sur hello `Models` dossier, **ajouter** > **classe**. Nommez-le `GeofenceBoundary.cs`. Après cela, copiez hello JSON à partir de la réponse hello API dont nous avons parlé dans la première section de hello et en cours d’utilisation de Visual Studio **modifier** > **Collage spécial** > **coller JSON en tant que Classes**. 

De cette façon, nous nous assurons que cet objet hello est désérialisée exactement telle qu’elle a été conçu. La classe obtenue doit ressembler à ceci :

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

Ensuite, ouvrez `Controllers` > `NotificationsController.cs`. Nous devons tootweak hello Post appel tooaccount de latitude et longitude de cible hello. Pour ce faire, ajoutez simplement signature de fonction deux chaînes toohello – `latitude` et `longitude`.

    public async Task<HttpResponseMessage> Post(string pns, [FromBody]string message, string to_tag, string latitude, string longitude)

Créez une classe dans le projet hello appelé `ApiHelper.cs` – nous allons l’utiliser intersections de tooconnect tooBing toocheck point limite. Implémentez une fonction `IsPointWithinBounds` de la manière suivante :

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
> Assurez-vous que toosubstitute hello API de point de terminaison avec hello URL de la requête que vous avez obtenu précédemment de hello centre de développement Bing (même règle s’applique toohello API clé). 
> 
> 

S’il existe des requêtes toohello de résultats, cela signifie que hello point spécifié se trouve dans les limites de hello de hello geofence, donc nous revenons `true`. S’il n’y a aucun résultat, Bing nous indique que le point de hello est en dehors de la frame de recherche hello, donc nous revenons `false`.

Dans `NotificationsController.cs`, créer une vérification juste avant l’instruction switch hello :

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

De cette façon, les notifications hello sont envoyée uniquement lorsque le point de hello se trouve dans les limites de hello.

## <a name="testing-push-notifications-in-hello-uwp-app"></a>Test des notifications push dans l’application de plateforme Windows universelle hello
Si vous revenez en application de plateforme Windows universelle toohello, nous devons maintenant être tootest en mesure de notifications. Au sein de hello `LocationHelper` de classe, créez une fonction – `SendLocationToBackend`:

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
> Échange hello `POST_URL` emplacement toohello de votre application web déployés que vous avez créée dans la section précédente de hello. Pour l’instant, il est OK toorun localement, mais lorsque vous travaillez sur le déploiement d’une version publique, vous devrez toohost avec un fournisseur externe.
> 
> 

Nous allons maintenant vous assurer que nous enregistrons application UWP de hello pour les notifications push. Dans Visual Studio, cliquez sur **projet** > **stocker** > **associer application hello store**.

![](./media/notification-hubs-geofence/vs-associate-with-store.png)

Une fois que vous vous connectez dans le compte de développeur tooyour, assurez-vous que vous sélectionnez une application existante ou créez un nouveau et lui associez les package hello. 

Accédez centre de développement toohello et application hello ouverts que vous venez de créer. Cliquez sur **Services** > **Notifications push** > **Services Microsoft Live**.

![](./media/notification-hubs-geofence/ms-live-services.png)

Sur le site de hello, prenez note de hello **Secret d’Application** et hello **SID du Package**. Vous devez à la fois dans hello portail Azure, ouvrez votre concentrateur de notification, cliquez sur **paramètres** > **Notification Services** > **Windows (WNS)**et entrez les informations de hello dans les champs hello requis.

![](./media/notification-hubs-geofence/notification-hubs-wns.png)

Cliquez sur **Save**(Enregistrer).

Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur **Références**, puis sélectionnez **Gérer les packages NuGet**. Nous devons tooadd un toohello référence **bibliothèque managée de Microsoft Azure Service Bus** – simplement rechercher `WindowsAzure.Messaging.Managed` et ajoutez-le tooyour projet.

![](./media/notification-hubs-geofence/vs-nuget.png)

À des fins de test, nous pouvons créer hello `MainPage_Loaded` Gestionnaire d’événements une fois encore et ajoutez cette tooit d’extrait de code :

    var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    var hub = new NotificationHub("HUB_NAME", "HUB_LISTEN_CONNECTION_STRING");
    var result = await hub.RegisterNativeAsync(channel.Uri);

    // Displays hello registration ID so you know it was successful
    if (result.RegistrationId != null)
    {
        Debug.WriteLine("Reg successful.");
    }

Hello ci-dessus inscrit application hello avec concentrateur de notification hello. Vous êtes prêt toogo ! 

Dans `LocationHelper`, à l’intérieur de hello `Geolocator_PositionChanged` gestionnaire, vous pouvez ajouter un élément de code de test qui force place emplacement hello hello geofence :

    await LocationHelper.SendLocationToBackend("wns", "TEST_USER", "TEST", "37.7746", "-122.3858");

Étant donné que nous ne réussissent pas les coordonnées réel hello (qui peuvent être dans les limites de hello moment hello) et que vous utilisez des valeurs de test prédéfinies, nous allons voir une notification s’affichent sur la mise à jour :

![](./media/notification-hubs-geofence/notification-hubs-test-notification.png)

## <a name="whats-next"></a>Et ensuite ?
Il existe quelques étapes que vous devrez peut-être toofollow dans toohello Ajout ci-dessus toomake assurer que les solutions hello sont prêt pour la production.

Tout d’abord, vous devrez peut-être tooensure que geofences sont dynamiques. Cette opération nécessite du travail supplémentaire avec hello API Bing dans l’ordre toobe tooupload en mesure de nouveau des limites au sein de la source de données existante hello. Consultez hello [documentation de l’API de Services de données spatiales Bing](https://msdn.microsoft.com/library/ff701734.aspx) pour plus d’informations sur le sujet de hello.

En second lieu, comme vous tooensure de travail que la remise de hello est effectuée toohello des participants à droite, vous souhaiterez peut-être tootarget leur via [marquage](notification-hubs-tags-segment-push-message.md).

solution Hello ci-dessus décrit un scénario dans lequel vous pourrez avoir un large éventail de plateformes cibles, afin que nous ne pas limiter hello géorepérage toosystem fonctionnalités. Ceci dit, hello plateforme Windows universelle offre des fonctions trop[détecter geofences droite out-of-the-box](https://msdn.microsoft.com/windows/uwp/maps-and-location/set-up-a-geofence).

Pour plus de détails concernant les fonctionnalités de Notification Hubs, consultez le [portail documentaire](https://azure.microsoft.com/documentation/services/notification-hubs/).

