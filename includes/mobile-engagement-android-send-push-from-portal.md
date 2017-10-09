### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a><span data-ttu-id="e6701-101">Grant Mobile Engagement accès tooyour clé API GCM</span><span class="sxs-lookup"><span data-stu-id="e6701-101">Grant Mobile Engagement access tooyour GCM API Key</span></span>
<span data-ttu-id="e6701-102">tooallow Mobile Engagement toosend des notifications push à votre place, vous devez toogrant il tooyour clé API d’accès.</span><span class="sxs-lookup"><span data-stu-id="e6701-102">tooallow Mobile Engagement toosend push notifications on your behalf, you need toogrant it access tooyour API Key.</span></span> <span data-ttu-id="e6701-103">Pour cela, en configurant et entrer votre clé dans le portail Mobile Engagement de hello.</span><span class="sxs-lookup"><span data-stu-id="e6701-103">This is done by configuring and entering your key into hello Mobile Engagement portal.</span></span>

1. <span data-ttu-id="e6701-104">À partir de votre portail classique Azure, vérifiez dans l’application hello nous à utiliser pour ce projet, puis cliquez sur hello **Engage** bouton bas hello :</span><span class="sxs-lookup"><span data-stu-id="e6701-104">From your Azure Classic Portal, ensure you're in hello app we're using for this project, and then click hello **Engage** button at hello bottom:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. <span data-ttu-id="e6701-105">Puis cliquez sur hello **paramètres** -> **le Push natif** section tooenter votre clé GCM :</span><span class="sxs-lookup"><span data-stu-id="e6701-105">Then click hello **Settings** -> **Native Push** section tooenter your GCM Key:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. <span data-ttu-id="e6701-106">Cliquez sur hello **modifier** icône devant **clé API** Bonjour **GCM paramètres** section comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="e6701-106">Click hello **Edit** icon in front of **API Key** in hello **GCM Settings** section as shown below:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. <span data-ttu-id="e6701-107">Dans la fenêtre contextuelle hello, collez hello clé du serveur GCM vous avez obtenus avant et puis cliquez sur **Ok**.</span><span class="sxs-lookup"><span data-stu-id="e6701-107">In hello pop-up, paste hello GCM Server Key you obtained before and then click **Ok**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <span data-ttu-id="e6701-108"><a id="send"></a>Envoi d’une application tooyour de notification</span><span class="sxs-lookup"><span data-stu-id="e6701-108"><a id="send"></a>Send a notification tooyour app</span></span>
<span data-ttu-id="e6701-109">Nous allons maintenant créer une campagne de notification push simple qui envoie une application tooour de notification push.</span><span class="sxs-lookup"><span data-stu-id="e6701-109">We will now create a simple push notification campaign that sends a push notification tooour app.</span></span>

1. <span data-ttu-id="e6701-110">Accédez toohello **atteindre** onglet dans votre portail Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="e6701-110">Navigate toohello **REACH** tab in your Mobile Engagement portal.</span></span>
2. <span data-ttu-id="e6701-111">Cliquez sur **nouvelle annonce** toocreate votre campagne de notification push.</span><span class="sxs-lookup"><span data-stu-id="e6701-111">Click **New announcement** toocreate your push notification campaign.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. <span data-ttu-id="e6701-112">Vous pouvez configurer hello premier champ de votre campagne via hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e6701-112">Set up hello first field of your campaign through hello following steps:</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    <span data-ttu-id="e6701-113">a.</span><span class="sxs-lookup"><span data-stu-id="e6701-113">a.</span></span> <span data-ttu-id="e6701-114">Nommez votre campagne.</span><span class="sxs-lookup"><span data-stu-id="e6701-114">Name your campaign.</span></span>
   
    <span data-ttu-id="e6701-115">b.</span><span class="sxs-lookup"><span data-stu-id="e6701-115">b.</span></span> <span data-ttu-id="e6701-116">Sélectionnez hello **type de remise** en tant que *notification système -> Simple*: il s’agit type de notification push Android simple hello qui propose un titre et une petite ligne de texte.</span><span class="sxs-lookup"><span data-stu-id="e6701-116">Select hello **Delivery type** as *System notification -> Simple*: This is hello simple Android push notification type that features a title and a small line of text.</span></span>
   
    <span data-ttu-id="e6701-117">c.</span><span class="sxs-lookup"><span data-stu-id="e6701-117">c.</span></span> <span data-ttu-id="e6701-118">Sélectionnez **heure de remise** en tant que *tout moment* tooallow hello application tooreceive une notification si l’application hello est démarrée ou non.</span><span class="sxs-lookup"><span data-stu-id="e6701-118">Select **Delivery time** as *Any time* tooallow hello app tooreceive a notification whether hello app is started or not.</span></span>
   
    <span data-ttu-id="e6701-119">d.</span><span class="sxs-lookup"><span data-stu-id="e6701-119">d.</span></span> <span data-ttu-id="e6701-120">Bonjour de type texte hello notification **titre** qui sera en gras dans les push hello.</span><span class="sxs-lookup"><span data-stu-id="e6701-120">In hello notification text type hello **Title** which will be in bold in hello push.</span></span>
   
    <span data-ttu-id="e6701-121">e.</span><span class="sxs-lookup"><span data-stu-id="e6701-121">e.</span></span> <span data-ttu-id="e6701-122">Tapez ensuite votre **message**</span><span class="sxs-lookup"><span data-stu-id="e6701-122">Then type your **Message**</span></span>
4. <span data-ttu-id="e6701-123">Faites défiler vers le bas et hello **contenu** section, sélectionnez **Notification uniquement**.</span><span class="sxs-lookup"><span data-stu-id="e6701-123">Scroll down, and in hello **Content** section, select **Notification only**.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. <span data-ttu-id="e6701-124">Vous avez terminé possible de campagne paramètre hello plus simple.</span><span class="sxs-lookup"><span data-stu-id="e6701-124">You're done setting hello most basic campaign possible.</span></span> <span data-ttu-id="e6701-125">Maintenant défiler à nouveau vers le bas et cliquez sur hello **créer** bouton toosave votre campagne.</span><span class="sxs-lookup"><span data-stu-id="e6701-125">Now scroll down again and click hello **Create** button toosave your campaign.</span></span>
6. <span data-ttu-id="e6701-126">Dernière étape : cliquez sur **activer** tooactivate vos notifications push de toosend campagne.</span><span class="sxs-lookup"><span data-stu-id="e6701-126">Last step: click **Activate** tooactivate your campaign toosend push notifications.</span></span>
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

