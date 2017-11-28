---
title: "Didacticiel sur l’utilisation de Notification Hubs pour envoyer les dernières nouvelles - iOS"
description: "Découvrez comment utiliser Azure Service Bus Notification Hubs pour envoyer des notifications de dernières nouvelles aux appareils iOS."
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
ms.openlocfilehash: dc47250db6fb3a2853dae24e02bda236154d93fb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="78bb8-103">Utilisation de Notification Hubs pour diffuser les dernières nouvelles</span><span class="sxs-lookup"><span data-stu-id="78bb8-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="78bb8-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="78bb8-104">Overview</span></span>
<span data-ttu-id="78bb8-105">Cette rubrique montre comment utiliser Azure Notification Hubs pour diffuser des notifications relatives aux dernières nouvelles vers une application iOS.</span><span class="sxs-lookup"><span data-stu-id="78bb8-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to an iOS app.</span></span> <span data-ttu-id="78bb8-106">Lorsque vous aurez terminé, vous pourrez vous inscrire aux catégories de dernières nouvelles qui vous intéressent et recevoir uniquement des notifications Push pour ces catégories.</span><span class="sxs-lookup"><span data-stu-id="78bb8-106">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="78bb8-107">Ce scénario est un modèle courant pour de nombreuses applications pour lesquelles des notifications doivent être envoyées à des groupes d'utilisateurs qui ont signalé antérieurement un intérêt, par exemple, lecteur RSS, applications pour fans de musique, etc.</span><span class="sxs-lookup"><span data-stu-id="78bb8-107">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="78bb8-108">Les scénarios de diffusion sont activés en incluant une ou plusieurs *balises* durant la création d’une inscription dans le hub de notification.</span><span class="sxs-lookup"><span data-stu-id="78bb8-108">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="78bb8-109">Lorsque des notifications sont envoyées à une balise, tous les appareils pour lesquels cette balise est inscrite reçoivent la notification.</span><span class="sxs-lookup"><span data-stu-id="78bb8-109">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="78bb8-110">Les balises étant de simples chaînes, il n’est pas nécessaire de les mettre en service à l’avance.</span><span class="sxs-lookup"><span data-stu-id="78bb8-110">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="78bb8-111">Pour plus d’informations sur les balises, consultez [Routage et expressions de balise Notification Hubs](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="78bb8-111">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78bb8-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="78bb8-112">Prerequisites</span></span>
<span data-ttu-id="78bb8-113">Cette rubrique s'appuie sur l'application que vous avez créée dans [Prise en main de Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="78bb8-113">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="78bb8-114">Avant de commencer ce didacticiel, vous devez suivre celui intitulé [Prise en main de Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="78bb8-114">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="78bb8-115">Ajout d’une sélection de catégories à l’application</span><span class="sxs-lookup"><span data-stu-id="78bb8-115">Add category selection to the app</span></span>
<span data-ttu-id="78bb8-116">La première étape consiste à ajouter à votre storyboard existant les éléments d'interface utilisateur qui permettent à l'utilisateur de sélectionner les catégories à inscrire.</span><span class="sxs-lookup"><span data-stu-id="78bb8-116">The first step is to add the UI elements to your existing storyboard that enable the user to select categories to register.</span></span> <span data-ttu-id="78bb8-117">Les catégories sélectionnées par un utilisateur sont stockées sur l'appareil.</span><span class="sxs-lookup"><span data-stu-id="78bb8-117">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="78bb8-118">Lorsque l’application démarre, une inscription d’appareil est créée dans votre hub de notification avec les catégories sélectionnées sous forme de balises.</span><span class="sxs-lookup"><span data-stu-id="78bb8-118">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="78bb8-119">Dans MainStoryboard_iPhone.storyboard, ajoutez les composants suivants de la bibliothèque d'objets :</span><span class="sxs-lookup"><span data-stu-id="78bb8-119">In your MainStoryboard_iPhone.storyboard add the following components from the object library:</span></span>
   
   * <span data-ttu-id="78bb8-120">une étiquette intitulée « Dernières nouvelles » ;</span><span class="sxs-lookup"><span data-stu-id="78bb8-120">A label with "Breaking News" text,</span></span>
   * <span data-ttu-id="78bb8-121">des étiquettes portant les intitulés de catégories « Monde », « Politiques », « Entreprise », « Technologies », « Science », « Sports » ;</span><span class="sxs-lookup"><span data-stu-id="78bb8-121">Labels with category texts "World", "Politics", "Business", "Technology", "Science", "Sports",</span></span>
   * <span data-ttu-id="78bb8-122">six commutateurs, un par catégorie, chacun défini sur **l’État** **désactivé** par défaut ;</span><span class="sxs-lookup"><span data-stu-id="78bb8-122">Six switches, one per category, set each switch **State** to be **Off** by default.</span></span>
   * <span data-ttu-id="78bb8-123">un bouton intitulé « S’abonner ».</span><span class="sxs-lookup"><span data-stu-id="78bb8-123">One button labeled "Subscribe"</span></span>
     
     <span data-ttu-id="78bb8-124">Votre storyboard doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="78bb8-124">Your storyboard should look as follows:</span></span>
     
     ![][3]
2. <span data-ttu-id="78bb8-125">Dans l'éditeur de l'Assistant, créez des outlets pour tous les commutateurs et appelez-les "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch".</span><span class="sxs-lookup"><span data-stu-id="78bb8-125">In the assistant editor, create outlets for all the switches and call them "WorldSwitch", "PoliticsSwitch", "BusinessSwitch", "TechnologySwitch", "ScienceSwitch", "SportsSwitch"</span></span>
3. <span data-ttu-id="78bb8-126">Créez une action pour le bouton intitulé « S’abonner ».</span><span class="sxs-lookup"><span data-stu-id="78bb8-126">Create an Action for your button called "subscribe".</span></span> <span data-ttu-id="78bb8-127">Le fichier ViewController.h doit désormais contenir le code suivant :</span><span class="sxs-lookup"><span data-stu-id="78bb8-127">Your ViewController.h should contain the following:</span></span>
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. <span data-ttu-id="78bb8-128">Créez une **classe Cocoa Touch** appelée `Notifications`.</span><span class="sxs-lookup"><span data-stu-id="78bb8-128">Create a new **Cocoa Touch Class** called `Notifications`.</span></span> <span data-ttu-id="78bb8-129">Copiez le code suivant dans la section de l’interface du fichier Notifications.h :</span><span class="sxs-lookup"><span data-stu-id="78bb8-129">Copy the following code in the interface section of the file Notifications.h:</span></span>
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. <span data-ttu-id="78bb8-130">Ajoutez la directive import suivante au fichier Notifications.m :</span><span class="sxs-lookup"><span data-stu-id="78bb8-130">Add the following import directive to Notifications.m:</span></span>
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. <span data-ttu-id="78bb8-131">Copiez le code suivant dans la section d’implémentation du fichier Notifications.m.</span><span class="sxs-lookup"><span data-stu-id="78bb8-131">Copy the following code in the implementation section of the file Notifications.m.</span></span>
   
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



    <span data-ttu-id="78bb8-132">Cette classe utilise le stockage local pour stocker et récupérer les catégories de nouvelles que cet appareil doit recevoir.</span><span class="sxs-lookup"><span data-stu-id="78bb8-132">This class uses local storage to store and retrieve the categories of news that this device will receive.</span></span> <span data-ttu-id="78bb8-133">Elle comporte également une méthode pour s’inscrire à ces catégories à l’aide de l’inscription de [modèle](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="78bb8-133">Also, it contains a method to register for these categories using a [Template](notification-hubs-templates-cross-platform-push-messages.md) registration.</span></span>

1. <span data-ttu-id="78bb8-134">Dans le fichier AppDelegate.h, ajoutez une instruction import pour Notifications.h et une propriété pour une instance de la classe Notifications :</span><span class="sxs-lookup"><span data-stu-id="78bb8-134">In the AppDelegate.h file, add an import statement for Notifications.h and add a property for an instance of the Notifications class:</span></span>
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. <span data-ttu-id="78bb8-135">Dans la méthode **didFinishLaunchingWithOptions** du fichier AppDelegate.m, ajoutez ce code pour initialiser l’instance de notifications au début de la méthode.</span><span class="sxs-lookup"><span data-stu-id="78bb8-135">In the **didFinishLaunchingWithOptions** method in AppDelegate.m, add the code to initialize the notifications instance at the beginning of the method.</span></span>  
   
    <span data-ttu-id="78bb8-136">Dans `HUBNAME` et `HUBLISTENACCESS` (définis dans hubinfo.h), le nom du hub de notification et la chaîne de connexion pour *DefaultListenSharedAccessSignature* obtenus précédemment doivent avoir remplacé les espaces réservés `<hub name>` et `<connection string with listen access>`.</span><span class="sxs-lookup"><span data-stu-id="78bb8-136">`HUBNAME` and `HUBLISTENACCESS` (defined in hubinfo.h) should already have the `<hub name>` and `<connection string with listen access>` placeholders replaced with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier</span></span>
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > <span data-ttu-id="78bb8-137">Les informations d’identification distribuées avec une application cliente n’étant généralement pas sécurisées, vous ne devez distribuer que la clé d’accès d’écoute avec votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="78bb8-137">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="78bb8-138">L'accès d'écoute permet à votre application de s'inscrire à des notifications, mais les inscriptions existantes ne peuvent pas être modifiées et les notifications ne peuvent pas être envoyées.</span><span class="sxs-lookup"><span data-stu-id="78bb8-138">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="78bb8-139">La clé d'accès complet est utilisée dans un service de serveur principal sécurisé pour l'envoi de notifications et la modification d'inscriptions existantes.</span><span class="sxs-lookup"><span data-stu-id="78bb8-139">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
3. <span data-ttu-id="78bb8-140">Dans la méthode **didRegisterForRemoteNotificationsWithDeviceToken** du fichier AppDelegate.m, remplacez le code de la méthode par le code suivant pour transmettre le jeton d’appareil à la classe Notifications.</span><span class="sxs-lookup"><span data-stu-id="78bb8-140">In the **didRegisterForRemoteNotificationsWithDeviceToken** method in AppDelegate.m, replace the code in the method with the following code to pass the device token to the notifications class.</span></span> <span data-ttu-id="78bb8-141">La classe Notifications effectue l’enregistrement pour les notifications avec les catégories.</span><span class="sxs-lookup"><span data-stu-id="78bb8-141">The notifications class will perform the registering for notifications with the categories.</span></span> <span data-ttu-id="78bb8-142">Si l’utilisateur modifie les sélections de catégorie, nous appelons la méthode `subscribeWithCategories` en réponse au bouton **S’abonner** pour mettre à jour les sections.</span><span class="sxs-lookup"><span data-stu-id="78bb8-142">If the user changes category selections, we call the `subscribeWithCategories` method in response to the **subscribe** button to update them.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="78bb8-143">Étant donné que le jeton d'appareil attribué par le service de notification Push Apple (APN, Apple Push Notification) peut être modifié à tout moment, vous devez vous inscrire aux notifications à intervalles réguliers pour éviter les défaillances de notification.</span><span class="sxs-lookup"><span data-stu-id="78bb8-143">Because the device token assigned by the Apple Push Notification Service (APNS) can chance at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="78bb8-144">Cet exemple s'inscrit aux notifications chaque fois que l'application démarre.</span><span class="sxs-lookup"><span data-stu-id="78bb8-144">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="78bb8-145">Pour les applications exécutées fréquemment, plus d'une fois par jour, vous pouvez probablement ignorer l'inscription afin de préserver la bande passante si moins d'un jour s'est écoulé depuis l'inscription précédente.</span><span class="sxs-lookup"><span data-stu-id="78bb8-145">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves the categories from local storage and requests a registration for these categories
        // each time the app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    <span data-ttu-id="78bb8-146">À ce stade, il est à noter qu'il ne doit pas y avoir d'autre code dans la méthode **didRegisterForRemoteNotificationsWithDeviceToken** .</span><span class="sxs-lookup"><span data-stu-id="78bb8-146">Note that at this point there should be no other code in the **didRegisterForRemoteNotificationsWithDeviceToken** method.</span></span>

1. <span data-ttu-id="78bb8-147">Les méthodes suivantes doivent être déjà présents dans AppDelegate.m à partir de la fin de la [prise en main des concentrateurs de Notification] [ get-started] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="78bb8-147">The following methods should already be present in AppDelegate.m from completing the [Get started with Notification Hubs][get-started] tutorial.</span></span>  <span data-ttu-id="78bb8-148">Si ce n’est pas le cas, veuillez les ajouter.</span><span class="sxs-lookup"><span data-stu-id="78bb8-148">If not, add them.</span></span>
   
    <span data-ttu-id="78bb8-149">-(void) MessageBox :(NSString *) titre message :(NSString *) messageText {}</span><span class="sxs-lookup"><span data-stu-id="78bb8-149">-(void)MessageBox:(NSString *)title message:(NSString *)messageText  {</span></span>
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    <span data-ttu-id="78bb8-150">}</span><span class="sxs-lookup"><span data-stu-id="78bb8-150">}</span></span>
   
   * <span data-ttu-id="78bb8-151">application (void) :(UIApplication *) application didReceiveRemoteNotification : (NSDictionary *) userInfo {NSLog (@ « % @ », userInfo) ;   [message self MessageBox:@"Notification » : [valueForKey:@"alert [userInfo objectForKey:@"aps »] »]] ; }</span><span class="sxs-lookup"><span data-stu-id="78bb8-151">(void)application:(UIApplication *)application didReceiveRemoteNotification:   (NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]]; }</span></span>
   
   <span data-ttu-id="78bb8-152">Cette méthode gère les notifications reçues lorsque l'application est en cours d'exécution en affichant tout simplement une **UIAlert**.</span><span class="sxs-lookup"><span data-stu-id="78bb8-152">This method handles notifications received when the app is running by displaying a simple **UIAlert**.</span></span>
2. <span data-ttu-id="78bb8-153">Dans le fichier ViewController.m, ajoutez une instruction import pour AppDelegate.h et copiez le code suivant dans la méthode **subscribe** générée par le Xcode.</span><span class="sxs-lookup"><span data-stu-id="78bb8-153">In ViewController.m, add a import statement for AppDelegate.h and copy the following code into the XCode-generated **subscribe** method.</span></span> <span data-ttu-id="78bb8-154">Ce code met à jour l’inscription aux notifications pour utiliser les nouvelles balises de catégories choisies par l’utilisateur dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="78bb8-154">This code will update the notification registration to use the new category tags the user has chosen in the user interface.</span></span>
   
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
   
   <span data-ttu-id="78bb8-155">Cette méthode crée une liste **NSMutableArray** de catégories et utilise la classe **Notifications** pour stocker la liste dans le stockage local et inscrire les balises correspondantes auprès du hub de notification.</span><span class="sxs-lookup"><span data-stu-id="78bb8-155">This method creates an **NSMutableArray** of categories and uses the **Notifications** class to store the list in the local storage and registers the corresponding tags with your notification hub.</span></span> <span data-ttu-id="78bb8-156">Lorsque des catégories sont modifiées, l'inscription est à nouveau créée avec les nouvelles catégories.</span><span class="sxs-lookup"><span data-stu-id="78bb8-156">When categories are changed, the registration is recreated with the new categories.</span></span>
3. <span data-ttu-id="78bb8-157">Dans ViewController.m, ajoutez le code suivant dans la méthode **viewDidLoad** pour définir l’interface utilisateur en fonction des catégories précédemment enregistrées.</span><span class="sxs-lookup"><span data-stu-id="78bb8-157">In ViewController.m, add the following code in the **viewDidLoad** method to set the user interface based on the previously saved categories.</span></span>

        // This updates the UI on startup based on the status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



<span data-ttu-id="78bb8-158">L’application peut désormais stocker un ensemble de catégories dans le stockage local de l’appareil utilisé pour s’inscrire auprès du Notification Hub au démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="78bb8-158">The app can now store a set of categories in the device local storage used to register with the notification hub whenever the app starts.</span></span>  <span data-ttu-id="78bb8-159">L’utilisateur peut modifier la sélection des catégories au démarrage et cliquer sur la méthode **subscribe** pour mettre à jour l’inscription de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="78bb8-159">The user can change the selection of categories at runtime and click the **subscribe** method to update the registration for the device.</span></span> <span data-ttu-id="78bb8-160">Ensuite, vous allez mettre à jour l’application pour envoyer les notifications de dernières nouvelles directement dans l’application elle-même.</span><span class="sxs-lookup"><span data-stu-id="78bb8-160">Next, you will update the app to send the breaking news notifications directly in the app itself.</span></span>

## <a name="optional-sending-tagged-notifications"></a><span data-ttu-id="78bb8-161">(Facultatif) Envoyer des notifications avec balises</span><span class="sxs-lookup"><span data-stu-id="78bb8-161">(optional) Sending tagged notifications</span></span>
<span data-ttu-id="78bb8-162">Si vous n’avez pas accès à Visual Studio, vous pouvez passer à la section suivante et envoyer des notifications à partir de l’application elle-même.</span><span class="sxs-lookup"><span data-stu-id="78bb8-162">If you don't have access to Visual Studio, you can skip to the next section and send notifications from the app itself.</span></span> <span data-ttu-id="78bb8-163">Vous pouvez également envoyer la notification de modèle appropriée à partir du [portail Azure Classic] à l’aide de l’onglet Débogage de votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="78bb8-163">You can also send the proper template notification from the [Azure Classic Portal] using the debug tab for your notification hub.</span></span> 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-the-device"></a><span data-ttu-id="78bb8-164">(Facultatif) Envoyer des notifications depuis l’appareil</span><span class="sxs-lookup"><span data-stu-id="78bb8-164">(optional) Send notifications from the device</span></span>
<span data-ttu-id="78bb8-165">Normalement, les notifications doivent être envoyées par un service principal. Toutefois, vous pouvez envoyer des notifications de dernières nouvelles directement à partir de l’application.</span><span class="sxs-lookup"><span data-stu-id="78bb8-165">Normally notifications would be sent by a backend service but, you can send breaking news notifications directly from the app.</span></span> <span data-ttu-id="78bb8-166">Pour cela, nous mettrons à jour le `SendNotificationRESTAPI` méthode que nous avons défini dans le [prise en main des concentrateurs de Notification] [ get-started] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="78bb8-166">To do this we will update the `SendNotificationRESTAPI` method that we defined in the [Get started with Notification Hubs][get-started] tutorial.</span></span>

1. <span data-ttu-id="78bb8-167">Dans ViewController.m, mettez à jour la méthode `SendNotificationRESTAPI` comme suit pour qu’elle accepte un paramètre pour la balise de catégorie et envoie une notification de [modèle](notification-hubs-templates-cross-platform-push-messages.md) adaptée.</span><span class="sxs-lookup"><span data-stu-id="78bb8-167">In ViewController.m update the `SendNotificationRESTAPI` method as follows so that it accepts a parameter for the category tag and sends the proper [template](notification-hubs-templates-cross-platform-push-messages.md) notification.</span></span>
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct the messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated the token to be used in the authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create the request to add the template notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add the category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send the REST request
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
2. <span data-ttu-id="78bb8-168">Dans la mise à jour ViewController.m, mettez à jour l’action **Envoyer des notifications** comme indiqué dans le code suivant.</span><span class="sxs-lookup"><span data-stu-id="78bb8-168">In ViewController.m update the **Send Notification** action as shown in the code that follows.</span></span> <span data-ttu-id="78bb8-169">Ainsi, les notifications sont envoyées à l’aide de chaque balise de manière individuelle vers plusieurs plateformes.</span><span class="sxs-lookup"><span data-stu-id="78bb8-169">So that it will send the notifications using each tag individually and send to multiple platforms.</span></span>

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send the message as breaking news for each category to WNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. <span data-ttu-id="78bb8-170">Régénérez votre projet et vérifiez qu’il n’existe aucune erreur de génération.</span><span class="sxs-lookup"><span data-stu-id="78bb8-170">Rebuild your project and make sure you have no build errors.</span></span>

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="78bb8-171">Exécution de l'application et génération de notifications</span><span class="sxs-lookup"><span data-stu-id="78bb8-171">Run the app and generate notifications</span></span>
1. <span data-ttu-id="78bb8-172">Cliquez sur le bouton Exécuter pour générer le projet et démarrer l’application.</span><span class="sxs-lookup"><span data-stu-id="78bb8-172">Press the Run button to build the project and start the app.</span></span> <span data-ttu-id="78bb8-173">Sélectionnez certaines options de dernières nouvelles pour vous y abonner, puis appuyez sur le bouton **S’abonner** .</span><span class="sxs-lookup"><span data-stu-id="78bb8-173">Select some breaking news options to subscribe to and then press the **Subscribe** button.</span></span> <span data-ttu-id="78bb8-174">Vous devez voir une boîte de dialogue indiquant les notifications auxquelles vous êtes abonné.</span><span class="sxs-lookup"><span data-stu-id="78bb8-174">You should see a dialog indicating the notifications have been subscribed to.</span></span>
   
    ![][1]
   
    <span data-ttu-id="78bb8-175">Lorsque vous sélectionnez **S’abonner**, l'application convertit les catégories sélectionnées en balises et demande une nouvelle inscription de l'appareil aux balises sélectionnées depuis le hub de notification.</span><span class="sxs-lookup"><span data-stu-id="78bb8-175">When you choose **Subscribe**, the app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span>
2. <span data-ttu-id="78bb8-176">Entrez un message à envoyer comme dernières nouvelles, puis appuyez sur le bouton **Envoyer une notification** .</span><span class="sxs-lookup"><span data-stu-id="78bb8-176">Enter a message to be sent as breaking news then press the **Send Notification** button.</span></span> <span data-ttu-id="78bb8-177">Vous pouvez également exécuter l’application console .NET pour générer des notifications.</span><span class="sxs-lookup"><span data-stu-id="78bb8-177">Alternatively, run the .NET console app to generate notifications.</span></span>
   
    ![][2]
3. <span data-ttu-id="78bb8-178">Chaque appareil abonné aux dernières nouvelles reçoit les notifications de dernières nouvelles que vous venez d’envoyer.</span><span class="sxs-lookup"><span data-stu-id="78bb8-178">Each device subscribed to breaking news will receive the breaking news notifications you just sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78bb8-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="78bb8-179">Next steps</span></span>
<span data-ttu-id="78bb8-180">Dans ce didacticiel, nous avons appris à diffuser les dernières nouvelles par catégorie.</span><span class="sxs-lookup"><span data-stu-id="78bb8-180">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="78bb8-181">Envisagez de suivre un des didacticiels suivants qui soulignent d’autres scénarios avancés Notification Hubs :</span><span class="sxs-lookup"><span data-stu-id="78bb8-181">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="78bb8-182">**[Utilisation de Notification Hubs pour diffuser les dernières nouvelles localisées]**</span><span class="sxs-lookup"><span data-stu-id="78bb8-182">**[Use Notification Hubs to broadcast localized breaking news]**</span></span>
  
    <span data-ttu-id="78bb8-183">Apprenez à développer l’application relative aux dernières nouvelles pour permettre l’envoi de notifications localisées.</span><span class="sxs-lookup"><span data-stu-id="78bb8-183">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
<span data-ttu-id="78bb8-184">[Utilisation de Notification Hubs pour diffuser les dernières nouvelles localisées]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="78bb8-184">[Use Notification Hubs to broadcast localized breaking news]: notification-hubs-ios-xplat-localized-apns-push-notification.md</span></span>
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
<span data-ttu-id="78bb8-185">[portail Azure Classic]: https://manage.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="78bb8-185">[Azure Classic Portal]: https://manage.windowsazure.com</span></span>
