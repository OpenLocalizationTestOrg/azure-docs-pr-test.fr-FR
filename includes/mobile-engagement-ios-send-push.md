### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a><span data-ttu-id="1944b-101">Accorder l’accès tooyour pousser le certificat tooMobile Engagement</span><span class="sxs-lookup"><span data-stu-id="1944b-101">Grant access tooyour Push Certificate tooMobile Engagement</span></span>
<span data-ttu-id="1944b-102">tooallow Mobile Engagement toosend des Notifications Push à votre place, vous devez toogrant il tooyour certificat d’accès.</span><span class="sxs-lookup"><span data-stu-id="1944b-102">tooallow Mobile Engagement toosend Push Notifications on your behalf, you need toogrant it access tooyour certificate.</span></span> <span data-ttu-id="1944b-103">Cela est fait en configurant et en entrant votre certificat dans le portail Mobile Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="1944b-103">This is done by configuring and entering your certificate into hello Mobile Engagement portal.</span></span> <span data-ttu-id="1944b-104">Assurez-vous d'obtenir votre certificat .p12 comme expliqué dans la [documentation d'Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span><span class="sxs-lookup"><span data-stu-id="1944b-104">Make sure you obtain your .p12 certificate as explained in [Apple's documentation](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)</span></span>

1. <span data-ttu-id="1944b-105">Accédez portail Mobile Engagement de tooyour.</span><span class="sxs-lookup"><span data-stu-id="1944b-105">Navigate tooyour Mobile Engagement portal.</span></span> <span data-ttu-id="1944b-106">Vérifiez que vous êtes dans hello correct, puis cliquez sur hello **Engage** bouton bas hello :</span><span class="sxs-lookup"><span data-stu-id="1944b-106">Ensure you're in hello correct and then click on hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. <span data-ttu-id="1944b-107">Cliquez sur hello **paramètres** page de votre portail du projet.</span><span class="sxs-lookup"><span data-stu-id="1944b-107">Click on hello **Settings** page in your Engagement Portal.</span></span> <span data-ttu-id="1944b-108">À partir de là, cliquez sur hello **le Push natif** section tooupload votre certificat p12 :</span><span class="sxs-lookup"><span data-stu-id="1944b-108">From there click on hello **Native Push** section tooupload your p12 certificate:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. <span data-ttu-id="1944b-109">Sélectionnez votre p12, téléchargez-le et tapez votre mot de passe :</span><span class="sxs-lookup"><span data-stu-id="1944b-109">Select your p12, upload it and type your password:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <span data-ttu-id="1944b-110"><a id="send"></a>Envoi d’une application tooyour de notification</span><span class="sxs-lookup"><span data-stu-id="1944b-110"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="1944b-111">Nous allons maintenant créer une campagne de Notification Push simple qui envoie une application de tooour par émission de données :</span><span class="sxs-lookup"><span data-stu-id="1944b-111">We will now create a simple Push Notification campaign that will send a push tooour app:</span></span>

1. <span data-ttu-id="1944b-112">Accédez toohello **atteindre** onglet dans votre portail Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1944b-112">Navigate toohello **Reach** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="1944b-113">Cliquez sur **nouvelle annonce** toocreate votre campagne push</span><span class="sxs-lookup"><span data-stu-id="1944b-113">Click **New Announcement** toocreate your push campaign</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. <span data-ttu-id="1944b-114">Le programme d’installation hello premiers champs de votre campagne :</span><span class="sxs-lookup"><span data-stu-id="1944b-114">Setup hello first fields of your campaign:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * <span data-ttu-id="1944b-115">Entrez un **nom** pour votre campagne.</span><span class="sxs-lookup"><span data-stu-id="1944b-115">Provide a **Name** for your campaign</span></span> 
   * <span data-ttu-id="1944b-116">Sélectionnez hello **heure de remise** en tant que **hors de l’application uniquement**: il s’agit hello Apple push notification type simple qui propose du texte.</span><span class="sxs-lookup"><span data-stu-id="1944b-116">Select hello **Delivery time** as **Out of app only**: this is hello simple Apple push notification type that features some text.</span></span>
   * <span data-ttu-id="1944b-117">Dans le texte de notification hello, tapez Bonjour première **titre** qui sera hello première ligne de commande de hello.</span><span class="sxs-lookup"><span data-stu-id="1944b-117">In hello notification text, type first hello **Title** which will be hello first line in hello push.</span></span>
   * <span data-ttu-id="1944b-118">Puis tapez votre **Message** qui sera la deuxième ligne de hello</span><span class="sxs-lookup"><span data-stu-id="1944b-118">Then type your **Message** which will be hello second line</span></span>
4. <span data-ttu-id="1944b-119">Faites défiler et Bonjour section de contenu, sélectionnez **Notification uniquement**</span><span class="sxs-lookup"><span data-stu-id="1944b-119">Scroll down, and in hello content section select **Notification only**</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. <span data-ttu-id="1944b-120">Vous avez terminé la campagne de paramètre hello plus simple.</span><span class="sxs-lookup"><span data-stu-id="1944b-120">You're done setting hello most basic campaign.</span></span> <span data-ttu-id="1944b-121">Maintenant faites défiler la liste et cliquez sur **créer** bouton toosave votre campagne de notification push.</span><span class="sxs-lookup"><span data-stu-id="1944b-121">Now scroll down and click on **Create** button toosave your push notification campaign.</span></span> 
6. <span data-ttu-id="1944b-122">-Cliquez sur **activer** toosend de notifications push.</span><span class="sxs-lookup"><span data-stu-id="1944b-122">Finally - click on **Activate** toosend push notification.</span></span> 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. <span data-ttu-id="1944b-123">Vous serez en mesure de recevoir une notification de hello sur votre appareil iOS dans le centre de notification hello hello suivante :</span><span class="sxs-lookup"><span data-stu-id="1944b-123">You will be able receive hello notification on your iOS device in hello notification center like hello following:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. <span data-ttu-id="1944b-124">Si vous avez une Apple Watch associé à cet appareil iOS vous voyez ensuite hello notification sur votre Apple Watch :</span><span class="sxs-lookup"><span data-stu-id="1944b-124">If you have an Apple Watch paired with this iOS device then you will see hello notification on your Apple Watch:</span></span>
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

