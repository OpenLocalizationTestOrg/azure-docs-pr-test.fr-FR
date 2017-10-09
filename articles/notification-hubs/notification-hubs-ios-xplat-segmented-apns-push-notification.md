---
title: "aaaNotification concentrateurs dernières actualités didacticiel - iOS"
description: "Découvrez comment toouse toosend de concentrateurs de Notification Azure Service Bus avec rupture des appareils de nouvelles notifications tooiOS."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="c4a7d-103">Utilisez toosend concentrateurs de Notification dernières actualités</span><span class="sxs-lookup"><span data-stu-id="c4a7d-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="c4a7d-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c4a7d-104">Overview</span></span>
<span data-ttu-id="c4a7d-105">Cette rubrique vous montre comment toouse Azure Notification Hubs toobroadcast avec rupture nouvelles notifications tooan iOS application.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooan iOS app.</span></span> <span data-ttu-id="c4a7d-106">Lorsque vous avez terminé, vous être en mesure de tooregister la rupture des catégories d’actualités que vous intéressez et recevoir des notifications push uniquement pour ces catégories.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-106">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="c4a7d-107">Ce scénario est courant pour de nombreuses applications où les notifications ont toogroups toobe envoyé d’utilisateurs qui ont précédemment été déclaré intérêt, par exemple, lecteur RSS, les applications pour des ventilateurs de musique, etc..</span><span class="sxs-lookup"><span data-stu-id="c4a7d-107">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="c4a7d-108">Scénarios de diffusion sont activés en incluant un ou plusieurs *balises* lors de la création d’un enregistrement dans le hub de notification hello.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="c4a7d-109">Lorsque les notifications sont envoyées tooa balise, tous les appareils qui ont inscrit pour la balise de hello seront recevoir une notification de hello.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-109">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="c4a7d-110">Étant donné que les balises sont simplement des chaînes, ils n’ont pas toobe configuré à l’avance.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-110">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="c4a7d-111">Pour plus d’informations sur les balises, consultez trop[le routage des concentrateurs de Notification et les Expressions de balises](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="c4a7d-111">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4a7d-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c4a7d-112">Prerequisites</span></span>
<span data-ttu-id="c4a7d-113">Cette rubrique s’appuie sur l’application hello que vous avez créé dans [prise en main des concentrateurs de Notification][get-started].</span><span class="sxs-lookup"><span data-stu-id="c4a7d-113">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="c4a7d-114">Avant de commencer ce didacticiel, vous devez suivre celui intitulé [Prise en main de Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="c4a7d-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="c4a7d-115">Ajouter une application de toohello de sélection de catégorie</span><span class="sxs-lookup"><span data-stu-id="c4a7d-115">Add category selection toohello app</span></span>
<span data-ttu-id="c4a7d-116">première étape de Hello est tooadd hello UI éléments tooyour storyboard existant qui permettent de hello utilisateur tooselect catégories tooregister.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-116">hello first step is tooadd hello UI elements tooyour existing storyboard that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="c4a7d-117">catégories de Hello sélectionnées par un utilisateur sont stockées sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-117">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="c4a7d-118">Au démarrage de l’application hello, une inscription de périphérique est créée dans votre concentrateur de notification avec les catégories de hello sélectionné sous forme de balises.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-118">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="c4a7d-119">Dans votre MainStoryboard_iPhone.storyboard ajoutez hello suivant des composants à partir de la bibliothèque d’objets hello :</span><span class="sxs-lookup"><span data-stu-id="c4a7d-119">In your MainStoryboard_iPhone.storyboard add hello following components from hello object library:</span></span>
   
   * <span data-ttu-id="c4a7d-120">une étiquette intitulée « Dernières nouvelles » ;</span><span class="sxs-lookup"><span data-stu-id="c4a7d-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="c4a7d-121">des étiquettes portant les intitulés de catégories « Monde », « Politiques », « Entreprise », « Technologies », « Science », « Sports » ;</span><span class="sxs-lookup"><span data-stu-id="c4a7d-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="c4a7d-122">Six commutateurs, un par catégorie, définissez chaque commutateur **état** toobe **hors** par défaut.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-122">Six switches, one per category, set each switch **State** toobe **Off** by default.</span></span>
   * <span data-ttu-id="c4a7d-123">un bouton intitulé « S’abonner ».</span><span class="sxs-lookup"><span data-stu-id="c4a7d-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="c4a7d-124">Votre storyboard doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="c4a7d-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="c4a7d-125">Dans l’éditeur de l’assistant hello, créer prises pour tous les commutateurs hello et les appeler « WorldSwitch », « PoliticsSwitch », « BusinessSwitch », « TechnologySwitch », « ScienceSwitch », « SportsSwitch »</span><span class="sxs-lookup"><span data-stu-id="c4a7d-125">In hello assistant editor, create outlets for all hello switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="c4a7d-126">Créez une action pour le bouton intitulé « S’abonner ».</span><span class="sxs-lookup"><span data-stu-id="c4a7d-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="c4a7d-127">Votre ViewController.h doit contenir des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="c4a7d-127">Your ViewController.h should contain hello following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="c4a7d-128">Créez une **classe Cocoa Touch** appelée `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="c4a7d-129">Copiez hello suivant de code dans la section d’interface hello du fichier de hello Notifications.h :</span><span class="sxs-lookup"><span data-stu-id="c4a7d-129">Copy hello following code in hello interface section of hello file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="c4a7d-130">Ajoutez hello suivant tooNotifications.m directive d’importation :</span><span class="sxs-lookup"><span data-stu-id="c4a7d-130">Add hello following import directive tooNotifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="c4a7d-131">Copiez hello suivant de code dans la section d’implémentation hello du fichier de hello Notifications.m.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-131">Copy hello following code in hello implementation section of hello file Notifications.m.</span></span>
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    <span data-ttu-id="c4a7d-132">Cette classe utilise le stockage local toostore et récupérer des catégories hello de news reçoit cet appareil.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-132">This class uses local storage toostore and retrieve hello categories of news that this device will receive.</span></span> <span data-ttu-id="c4a7d-133">Il contient également un tooregister de méthode pour ces catégories en utilisant un [modèle](notification-hubs-templates-cross-platform-push-messages.md) l’inscription.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-133">Also, it contains a method tooregister for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="c4a7d-134">Dans le fichier de AppDelegate.h hello, ajoutez une instruction d’importation pour Notifications.h et ajouter une propriété d’une instance de la classe de Notifications de hello :</span><span class="sxs-lookup"><span data-stu-id="c4a7d-134">In hello AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of hello Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="c4a7d-135">Bonjour **didFinishLaunchingWithOptions** méthode dans AppDelegate.m, ajoutez instance de notifications hello code tooinitialize hello début hello de méthode hello.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-135">In hello **didFinishLaunchingWithOptions** method in AppDelegate.m, add hello code tooinitialize hello notifications instance at hello beginning of hello method.</span></span>  
   
    <span data-ttu-id="c4a7d-136">`HUBNAME`et `HUBLISTENACCESS` (défini dans hubinfo.h) doit déjà avoir hello `<hub name>` et `<connection string with listen access>` des espaces réservés est remplacé par votre notification hub hello et nom de chaîne de connexion pour *DefaultListenSharedAccessSignature*que vous avez obtenu précédemment</span><span class="sxs-lookup"><span data-stu-id="c4a7d-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have hello `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="c4a7d-137">Étant donné que les informations d’identification qui sont distribuées avec une application cliente ne sont pas sécurisées en règle générale, vous devez distribuer clé hello pour l’accès en écoute avec votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="c4a7d-138">Écouter access active que tooregister de votre application pour les notifications, mais les inscriptions existantes ne peut pas être modifié et des notifications ne peut pas être envoyées.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-138">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="c4a7d-139">clé d’accès complet de Hello est utilisée dans un service principal sécurisé pour envoyer des notifications et la modification des enregistrements existants.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-139">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="c4a7d-140">Bonjour **didRegisterForRemoteNotificationsWithDeviceToken** méthode dans AppDelegate.m, remplacez code hello dans la méthode hello hello après la classe de code toopass hello périphérique jeton toohello des notifications.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-140">In hello **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace hello code in hello method with hello following code toopass hello device token toohello notifications class.</span></span> <span data-ttu-id="c4a7d-141">classe de notifications Hello effectuera hello inscription aux notifications avec les catégories de hello.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-141">hello notifications class will perform hello registering for notifications with hello categories.</span></span> <span data-ttu-id="c4a7d-142">Si l’utilisateur de hello modifie les sélections de catégorie, nous appelons hello `subscribeWithCategories` méthode dans la réponse toohello **s’abonner** bouton tooupdate les.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-142">If hello user changes category selections, we call hello `subscribeWithCategories` method in response toohello **subscribe** button tooupdate them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c4a7d-143">Étant donné que le jeton du périphérique hello attribué par hello Apple Push Notification Service (APNS) pouvez chance à tout moment, vous devez inscrire pour les notifications fréquemment tooavoid les échecs de notification.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-143">Because hello device token assigned by hello Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="c4a7d-144">Cet exemple inscrit pour la notification chaque fois que cette application hello démarre.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-144">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="c4a7d-145">Pour les applications qui sont exécutées fréquemment, plusieurs fois par jour, vous pouvez probablement ignorer la bande passante de l’inscription toopreserve si l’enregistrement précédent de hello remonte à moins d’un jour.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-145">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="c4a7d-146">Notez qu’à ce stade il ne doit y avoir aucun autre code Bonjour **didRegisterForRemoteNotificationsWithDeviceToken** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c4a7d-146">Note that at this point there should be no other code in hello **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="c4a7d-147">Hello méthodes suivantes doivent déjà être présentes dans AppDelegate.m à partir de la fin de hello [prise en main des concentrateurs de Notification] [ get-started] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-147">hello following methods should already be present in AppDelegate.m from completing hello [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="c4a7d-148">Si ce n’est pas le cas, veuillez les ajouter.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-148">If not, add them.</span></span>
   
    <span data-ttu-id="c4a7d-149">-(void) MessageBox :(NSString *) titre message :(NSString *) messageText {}</span><span class="sxs-lookup"><span data-stu-id="c4a7d-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="c4a7d-150">}</span><span class="sxs-lookup"><span data-stu-id="c4a7d-150">}</span></span>
   
   * <span data-ttu-id="c4a7d-151">application (void) :(UIApplication *) application didReceiveRemoteNotification : (NSDictionary *) userInfo {NSLog (@ « % @ », userInfo) ;   [message self MessageBox:@"Notification » : [valueForKey:@"alert [userInfo objectForKey:@"aps »] »]] ; }</span><span class="sxs-lookup"><span data-stu-id="c4a7d-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="c4a7d-152">Cette méthode gère les notifications reçues lors de l’application hello est en cours d’exécution en affichant un simple **UIAlert**.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-152">This method handles notifications received when hello app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="c4a7d-153">Dans ViewController.m, ajoutez une instruction d’importation pour AppDelegate.h et copie hello après le code dans hello XCode généré **s’abonner** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c4a7d-153">In ViewController.m, add a import statement for AppDelegate.h and copy hello following code into hello XCode-generated **subscribe** method.</span></span> <span data-ttu-id="c4a7d-154">Ce code met à jour hello notification d’enregistrement toouse hello nouvelle catégorie balises hello l’utilisateur a choisi dans l’interface utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-154">This code will update hello notification registration toouse hello new category tags hello user has chosen in hello user interface.</span></span>
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   <span data-ttu-id="c4a7d-155">Cette méthode crée un **NSMutableArray** de catégories et les utilisations hello **Notifications** liste hello classe toostore hello local stockage et les registres hello balises correspondantes avec votre concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-155">This method creates an **NSMutableArray** of categories and uses hello **Notifications** class toostore hello list in hello local storage and registers hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="c4a7d-156">Si des catégories sont modifiées, l’inscription de hello est recréée avec les nouvelles catégories de hello.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-156">When categories are changed, hello registration is recreated with hello new categories.</span></span>
3. <span data-ttu-id="c4a7d-157">Dans ViewController.m, ajoutez hello suivant code Bonjour **viewDidLoad** interface utilisateur de méthode tooset hello en fonction de catégories de hello précédemment enregistré.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-157">In ViewController.m, add hello following code in hello **viewDidLoad** method tooset hello user interface based on hello previously saved categories.</span></span>

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="c4a7d-158">application Hello peut maintenant stocker un ensemble de catégories dans tooregister de stockage local utilisé hello appareil avec un concentrateur de notification hello à chaque démarrage de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-158">hello app can now store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello app starts.</span></span>  <span data-ttu-id="c4a7d-159">utilisateur de Hello peut modifier la sélection hello des catégories lors de l’exécution et cliquez sur hello **s’abonner** méthode tooupdate hello l’inscription de périphérique de hello.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-159">hello user can change hello selection of categories at runtime and click hello **subscribe** method tooupdate hello registration for hello device.</span></span> <span data-ttu-id="c4a7d-160">Ensuite, vous mettrez à jour hello de toosend application hello avec rupture des notifications sur l’actualité directement dans l’application hello proprement dit.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-160">Next, you will update hello app toosend hello breaking news notifications directly in hello app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="c4a7d-161">(Facultatif) Envoyer des notifications avec balises</span><span class="sxs-lookup"><span data-stu-id="c4a7d-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="c4a7d-162">Si vous n’avez pas accès tooVisual Studio, vous pouvez ignorer la section suivante de toohello et envoyer des notifications à partir de l’application hello proprement dit.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-162">If you don't have access tooVisual Studio, you can skip toohello next section and send notifications from hello app itself.</span></span> <span data-ttu-id="c4a7d-163">Vous pouvez également envoyer une notification de modèle approprié hello de hello [portail classique Azure] à l’aide d’onglet débogage de hello pour votre concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-163">You can also send hello proper template notification from hello [Azure Classic Portal] using hello debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a><span data-ttu-id="c4a7d-164">(facultatif) Envoyer des notifications à partir de l’appareil de hello</span><span class="sxs-lookup"><span data-stu-id="c4a7d-164">(optional) Send notifications from hello device</span></span>
<span data-ttu-id="c4a7d-165">Normalement des notifications sont envoyées par un service principal, mais vous pouvez envoyer des notifications sur l’actualité directement à partir de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from hello app.</span></span> <span data-ttu-id="c4a7d-166">toodo cela nous mettrons à jour hello `SendNotificationRESTAPI` méthode que nous avons défini Bonjour [prise en main des concentrateurs de Notification] [ get-started] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-166">toodo this we will update hello `SendNotificationRESTAPI` method that we defined in hello [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="c4a7d-167">Bonjour de mise à jour ViewController.m `SendNotificationRESTAPI` méthode comme suit afin qu’il accepte un paramètre pour l’étiquette de catégorie hello et envoie hello approprié [modèle](notification-hubs-templates-cross-platform-push-messages.md) notification.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-167">In ViewController.m update hello `SendNotificationRESTAPI` method as follows so that it accepts a parameter for hello category tag and sends hello proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add hello category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                       completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
               {
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                   if (error || httpResponse.statusCode != 200)
                   {
                       NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                   }
                   if (data != NULL)
                   {
                       //xmlParser = [[NSXMLParser alloc] initWithData:data];
                       //[xmlParser setDelegate:self];
                       //[xmlParser parse];
                   }
               }];
   
            [dataTask resume];
        }
2. <span data-ttu-id="c4a7d-168">Bonjour de mise à jour ViewController.m **envoyer une Notification** action, comme indiqué dans le code hello qui suit.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-168">In ViewController.m update hello **Send Notification** action as shown in hello code that follows.</span></span> <span data-ttu-id="c4a7d-169">Afin qu’il envoie des notifications de hello à l’aide de chaque balise individuellement et envoyer toomultiple plateformes.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-169">So that it will send hello notifications using each tag individually and send toomultiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="c4a7d-170">Régénérez votre projet et vérifiez qu’il n’existe aucune erreur de génération.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="c4a7d-171">Exécutez l’application hello et générer des notifications</span><span class="sxs-lookup"><span data-stu-id="c4a7d-171">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="c4a7d-172">Hello de presse exécuter bouton toobuild hello projet et démarrer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-172">Press hello Run button toobuild hello project and start hello app.</span></span> <span data-ttu-id="c4a7d-173">Sélectionnez certains tooand toosubscribe de rupture nouvelles options et appuyez sur hello **s’abonner** bouton.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-173">Select some breaking news options toosubscribe tooand then press hello **Subscribe** button.</span></span> <span data-ttu-id="c4a7d-174">Vous devez voir une boîte de dialogue indiquant hello notifications sont abonnées.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-174">You should see a dialog indicating hello notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="c4a7d-175">Lorsque vous choisissez **s’abonner**, hello des catégories d’applications convertit hello sélectionné dans les balises et demande une nouvelle inscription de périphérique pour les balises de hello sélectionné à partir du hub de notification hello.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-175">When you choose **Subscribe**, hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span>
2. <span data-ttu-id="c4a7d-176">Entrez un toobe message envoyé comme informations de dernière minute puis appuyez sur hello **envoyer une Notification** bouton.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-176">Enter a message toobe sent as breaking news then press hello **Send Notification** button.</span></span> <span data-ttu-id="c4a7d-177">Vous pouvez également exécuter notifications de toogenerate l’application console hello .NET.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-177">Alternatively, run hello .NET console app toogenerate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="c4a7d-178">Chaque news toobreaking de périphérique abonné recevra les notifications sur l’actualité hello que vous venez d’envoyer.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-178">Each device subscribed toobreaking news will receive hello breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4a7d-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c4a7d-179">Next steps</span></span>
<span data-ttu-id="c4a7d-180">Dans ce didacticiel, nous l’avons vu comment toobroadcast actualités par catégorie.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-180">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="c4a7d-181">Envisager d’effectuer une des hello suivant des didacticiels qui mettent en évidence les autres scénarios avancés de concentrateurs de Notification :</span><span class="sxs-lookup"><span data-stu-id="c4a7d-181">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="c4a7d-182">**[Utiliser les informations de dernière minute toobroadcast localisée de concentrateurs de Notification]**</span><span class="sxs-lookup"><span data-stu-id="c4a7d-182">**[Use Notification Hubs toobroadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="c4a7d-183">Découvrez comment hello tooexpand dernières actualités application tooenable envoi localisée des notifications.</span><span class="sxs-lookup"><span data-stu-id="c4a7d-183">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Utiliser les informations de dernière minute toobroadcast localisée de concentrateurs de Notification]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[portail classique Azure]: https://manage.windowsazure.com
