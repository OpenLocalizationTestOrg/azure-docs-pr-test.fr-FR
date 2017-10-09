

## <a name="generate-hello-certificate-signing-request-file"></a><span data-ttu-id="444cb-101">Générer le fichier de demande de signature de certificat hello</span><span class="sxs-lookup"><span data-stu-id="444cb-101">Generate hello Certificate Signing Request file</span></span>
<span data-ttu-id="444cb-102">Hello Apple Push Notification Service (APNS) utilise des certificats tooauthenticate vos notifications push.</span><span class="sxs-lookup"><span data-stu-id="444cb-102">hello Apple Push Notification Service (APNS) uses certificates tooauthenticate your push notifications.</span></span> <span data-ttu-id="444cb-103">Suivez ces toosend de certificat instructions toocreate hello push nécessaires et recevoir des notifications.</span><span class="sxs-lookup"><span data-stu-id="444cb-103">Follow these instructions toocreate hello necessary push certificate toosend and receive notifications.</span></span> <span data-ttu-id="444cb-104">Pour plus d’informations sur ces concepts, consultez officielle de hello [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span><span class="sxs-lookup"><span data-stu-id="444cb-104">For more information on these concepts see hello official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="444cb-105">Générer le fichier de demande de signature de certificat (CSR) hello, qui est utilisé par Apple toogenerate un certificat signé par émission de données.</span><span class="sxs-lookup"><span data-stu-id="444cb-105">Generate hello Certificate Signing Request (CSR) file, which is used by Apple toogenerate a signed push certificate.</span></span>

1. <span data-ttu-id="444cb-106">Sur votre Mac, exécutez hello outil de trousseau d’accès.</span><span class="sxs-lookup"><span data-stu-id="444cb-106">On your Mac, run hello Keychain Access tool.</span></span> <span data-ttu-id="444cb-107">Il peut être ouverte à partir de hello **utilitaires** dossier ou hello **autres** dossier sur la zone de lancement hello.</span><span class="sxs-lookup"><span data-stu-id="444cb-107">It can be opened from hello **Utilities** folder or hello **Other** folder on hello launch pad.</span></span>
2. <span data-ttu-id="444cb-108">Cliquez sur **Trousseaux d'accès**, développez **Assistant de certification**, puis cliquez sur **Demander un certificat à une autorité de certification**.</span><span class="sxs-lookup"><span data-stu-id="444cb-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="444cb-109">Sélectionnez votre **adresse de messagerie utilisateur** et **nom commun** , assurez-vous que **enregistré toodisk** est sélectionné, puis cliquez sur **continuer**.</span><span class="sxs-lookup"><span data-stu-id="444cb-109">Select your **User Email Address** and **Common Name** , make sure that **Saved toodisk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="444cb-110">Laissez hello **adresse de messagerie d’autorité de certification** champ vide car il n’est pas requis.</span><span class="sxs-lookup"><span data-stu-id="444cb-110">Leave hello **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="444cb-111">Tapez un nom pour le fichier de demande de signature de certificat (CSR) hello dans **enregistrer en tant que**, sélectionnez l’emplacement de hello dans **où**, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="444cb-111">Type a name for hello Certificate Signing Request (CSR) file in **Save As**, select hello location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="444cb-112">Ce fichier de signature de certificat hello enregistre dans l’emplacement de hello sélectionné ; emplacement par défaut de Hello est hello bureau.</span><span class="sxs-lookup"><span data-stu-id="444cb-112">This saves hello CSR file in hello selected location; hello default location is in hello Desktop.</span></span> <span data-ttu-id="444cb-113">N’oubliez pas d’emplacement de hello choisi pour ce fichier.</span><span class="sxs-lookup"><span data-stu-id="444cb-113">Remember hello location chosen for this file.</span></span>

<span data-ttu-id="444cb-114">Ensuite, vous l’inscrivez auprès d’Apple, activer les notifications push et télécharger cette toocreate de signature de certificat exporté un certificat push.</span><span class="sxs-lookup"><span data-stu-id="444cb-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR toocreate a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="444cb-115">Inscription de votre application pour les notifications Push</span><span class="sxs-lookup"><span data-stu-id="444cb-115">Register your app for push notifications</span></span>
<span data-ttu-id="444cb-116">toobe toosend en mesure de push notifications tooan iOS application, vous devez inscrire votre application avec Apple et également s’inscrire pour des notifications push.</span><span class="sxs-lookup"><span data-stu-id="444cb-116">toobe able toosend push notifications tooan iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="444cb-117">Si vous n’avez pas encore inscrit votre application, accédez à toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> au hello Apple Developer Center, ouverture de session avec votre ID Apple, cliquez sur **identificateurs**, puis cliquez sur **ID d’application** et enfin cliquez sur hello  **+**  tooregister une nouvelle application de connexion.</span><span class="sxs-lookup"><span data-stu-id="444cb-117">If you have not already registered your app, navigate toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at hello Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on hello **+** sign tooregister a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="444cb-118">Mettre à jour hello suivant trois champs pour votre nouvelle application, puis cliquez sur **continuer**:</span><span class="sxs-lookup"><span data-stu-id="444cb-118">Update hello following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="444cb-119">**Nom**: tapez un nom descriptif pour votre application Bonjour **nom** champ hello **Description de l’ID d’application** section.</span><span class="sxs-lookup"><span data-stu-id="444cb-119">**Name**: Type a descriptive name for your app in hello **Name** field in hello **App ID Description** section.</span></span>
   * <span data-ttu-id="444cb-120">**Identificateur d’offres groupées**: sous hello **ID d’application explicite** section, entrez un **identificateur de lot** sous forme de hello `<Organization Identifier>.<Product Name>` comme indiqué dans hello [Distribution d’applications Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span><span class="sxs-lookup"><span data-stu-id="444cb-120">**Bundle Identifier**: Under hello **Explicit App ID** section, enter a **Bundle Identifier** in hello form `<Organization Identifier>.<Product Name>` as mentioned in hello [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="444cb-121">Hello *identifiant d’organisation* et *Product Name* vous utilisez doit correspondre à l’identificateur de l’organisation hello et nom de produit à utiliser lorsque vous créez votre projet XCode.</span><span class="sxs-lookup"><span data-stu-id="444cb-121">hello *Organization Identifier* and *Product Name* you use must match hello organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="444cb-122">Dans screeshot hello ci-dessous *NotificationHubs* est utilisé comme un identificateur de l’organisation et *GetStarted* est utilisé comme nom de produit hello.</span><span class="sxs-lookup"><span data-stu-id="444cb-122">In hello screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as hello product name.</span></span> <span data-ttu-id="444cb-123">S’assurer que cela correspond aux valeurs hello que vous utiliserez dans votre projet XCode permettra de vous toouse hello correct profil de publication avec XCode.</span><span class="sxs-lookup"><span data-stu-id="444cb-123">Making sure this matches hello values you will use in your XCode project will allow you toouse hello correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="444cb-124">**Notifications push**: vérification hello **des Notifications Push** option Bonjour **des Services d’application** section.</span><span class="sxs-lookup"><span data-stu-id="444cb-124">**Push Notifications**: Check hello **Push Notifications** option in hello **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="444cb-125">Cette opération génère votre ID d’application et vous demande des informations de hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="444cb-125">This generates your App ID and requests you tooconfirm hello information.</span></span> <span data-ttu-id="444cb-126">Cliquez sur **inscrire** tooconfirm hello nouvel ID d’application.</span><span class="sxs-lookup"><span data-stu-id="444cb-126">Click **Register** tooconfirm hello new App ID.</span></span>
     
      <span data-ttu-id="444cb-127">Une fois que vous cliquez sur **inscrire**, vous verrez hello **inscription Terminer** écran, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="444cb-127">Once you click **Register**, you will see hello **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="444cb-128">Cliquez sur **Done**.</span><span class="sxs-lookup"><span data-stu-id="444cb-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="444cb-129">Bonjour centre de développement, sous l’ID d’application, recherchez hello ID d’application que vous venez de créer et cliquez sur sa ligne.</span><span class="sxs-lookup"><span data-stu-id="444cb-129">In hello Developer Center, under App IDs, locate hello app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="444cb-130">Vous pouvez afficher les détails de l’application hello en cliquant sur l’ID de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="444cb-130">Clicking on hello app ID will display hello app details.</span></span> <span data-ttu-id="444cb-131">Cliquez sur hello **modifier** bouton bas hello.</span><span class="sxs-lookup"><span data-stu-id="444cb-131">Click hello **Edit** button at hello bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="444cb-132">Faites défiler bas toohello d’écran hello et cliquez sur hello **créer un certificat...**  sous la section de hello **développement le certificat SSL Push**.</span><span class="sxs-lookup"><span data-stu-id="444cb-132">Scroll toohello bottom of hello screen, and click hello **Create Certificate...** button under hello section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="444cb-133">Cela permet d’afficher l’assistant « Ajouter iOS de certificat » hello.</span><span class="sxs-lookup"><span data-stu-id="444cb-133">This displays hello "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="444cb-134">Ce didacticiel utilise un certificat de développement.</span><span class="sxs-lookup"><span data-stu-id="444cb-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="444cb-135">Hello même processus est utilisé lors de l’inscription d’un certificat de production.</span><span class="sxs-lookup"><span data-stu-id="444cb-135">hello same process is used when registering a production certificate.</span></span> <span data-ttu-id="444cb-136">Assurez-vous simplement que vous utilisez hello même type de certificat lors de l’envoi des notifications.</span><span class="sxs-lookup"><span data-stu-id="444cb-136">Just make sure that you use hello same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="444cb-137">Cliquez sur **choisir un fichier**, rechercher l’emplacement de toohello où vous avez enregistré le fichier CSR hello que vous avez créé dans la première tâche de hello, puis cliquez sur **générer**.</span><span class="sxs-lookup"><span data-stu-id="444cb-137">Click **Choose File**, browse toohello location where you saved hello CSR file that you created in hello first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="444cb-138">Une fois le certificat de hello est créé par le portail de hello, cliquez sur hello **télécharger** , puis cliquez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="444cb-138">After hello certificate is created by hello portal, click hello **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="444cb-139">Il télécharge hello certificat et l’enregistre tooyour ordinateur dans le dossier Téléchargements.</span><span class="sxs-lookup"><span data-stu-id="444cb-139">This downloads hello certificate and saves it tooyour computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="444cb-140">Par défaut, hello téléchargé un certificat de développement se nomme **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="444cb-140">By default, hello downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="444cb-141">Double-cliquez sur : certificat push téléchargé hello **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="444cb-141">Double-click hello downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="444cb-142">Cette commande installe un nouveau certificat hello dans hello trousseau, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="444cb-142">This installs hello new certificate in hello Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="444cb-143">nom Hello dans votre certificat peut être différent, mais il est précédé de **Apple développement iOS Services Push :**.</span><span class="sxs-lookup"><span data-stu-id="444cb-143">hello name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="444cb-144">Dans le trousseau d’accès, avec le bouton droit hello nouveau poussée du certificat que vous avez créé dans hello **certificats** catégorie.</span><span class="sxs-lookup"><span data-stu-id="444cb-144">In Keychain Access, right-click hello new push certificate that you created in hello **Certificates** category.</span></span> <span data-ttu-id="444cb-145">Cliquez sur **exporter**, nommez le fichier de hello, sélectionnez hello **.p12** mettre en forme, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="444cb-145">Click **Export**, name hello file, select hello **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="444cb-146">Rendre une note hello du nom de fichier et l’emplacement du certificat exporté .p12 de hello.</span><span class="sxs-lookup"><span data-stu-id="444cb-146">Make a note of hello file name and location of hello exported .p12 certificate.</span></span> <span data-ttu-id="444cb-147">Il s’agit de l’authentification tooenable utilisé avec APNS.</span><span class="sxs-lookup"><span data-stu-id="444cb-147">It will be used tooenable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="444cb-148">Ce didacticiel permet de créer un fichier QuickStart.p12.</span><span class="sxs-lookup"><span data-stu-id="444cb-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="444cb-149">Il est possible que le nom de votre fichier et son emplacement sont différents.</span><span class="sxs-lookup"><span data-stu-id="444cb-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a><span data-ttu-id="444cb-150">Créer un profil de configuration pour l’application hello</span><span class="sxs-lookup"><span data-stu-id="444cb-150">Create a provisioning profile for hello app</span></span>
1. <span data-ttu-id="444cb-151">Dans hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, sélectionnez **profils de configuration**, sélectionnez **tous les**, puis cliquez sur hello  **+**  bouton toocreate un nouveau profil.</span><span class="sxs-lookup"><span data-stu-id="444cb-151">Back in hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click hello **+** button toocreate a new profile.</span></span> <span data-ttu-id="444cb-152">Cette opération lance hello **ajouter Provisiong profil iOS** Assistant</span><span class="sxs-lookup"><span data-stu-id="444cb-152">This launches hello **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="444cb-153">Sélectionnez **iOS le développement d’applications** sous **développement** en tant que type de profil hello provisiong, puis cliquez sur **continuer**.</span><span class="sxs-lookup"><span data-stu-id="444cb-153">Select **iOS App Development** under **Development** as hello provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="444cb-154">Ensuite, sélectionnez ID d’application hello vous venez de créer à partir de hello **ID d’application** liste déroulante, puis cliquez sur **continuer**</span><span class="sxs-lookup"><span data-stu-id="444cb-154">Next, select hello app ID you just created from hello **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="444cb-155">Bonjour **sélectionner les certificats** écran, sélectionnez votre certificat habituelles de développement utilisé pour la signature de code, puis cliquez sur **continuer**.</span><span class="sxs-lookup"><span data-stu-id="444cb-155">In hello **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="444cb-156">Il ne s’agit pas de certificat de push de hello que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="444cb-156">This is not hello push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="444cb-157">Ensuite, sélectionnez hello **périphériques** toouse pour le test, puis cliquez sur **continuer**</span><span class="sxs-lookup"><span data-stu-id="444cb-157">Next, select hello **Devices** toouse for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="444cb-158">Enfin, choisissez un nom pour le profil hello dans **nom du profil**, cliquez sur **générer**.</span><span class="sxs-lookup"><span data-stu-id="444cb-158">Finally, pick a name for hello profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="444cb-159">Lors de la création de nouveau profil de configuration de hello cliquez sur toodownload et installer sur votre ordinateur de développement Xcode.</span><span class="sxs-lookup"><span data-stu-id="444cb-159">When hello new provisioning profile is created click toodownload it and install it on your Xcode development machine.</span></span> <span data-ttu-id="444cb-160">Cliquez ensuite sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="444cb-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
