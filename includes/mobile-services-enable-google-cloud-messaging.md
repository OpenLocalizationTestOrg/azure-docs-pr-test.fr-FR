
1. <span data-ttu-id="3dcc0-101">Accédez toohello [Google Cloud Console](https://console.developers.google.com/project), connectez-vous avec vos informations d’identification du compte Google.</span><span class="sxs-lookup"><span data-stu-id="3dcc0-101">Navigate toohello [Google Cloud Console](https://console.developers.google.com/project), sign in with your Google account credentials.</span></span> 
2. <span data-ttu-id="3dcc0-102">Cliquez sur **Créer un projet**, saisissez un nom de projet, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="3dcc0-102">Click **Create Project**, type a project name, then click **Create**.</span></span> <span data-ttu-id="3dcc0-103">Le cas échéant, effectuer hello vérification par SMS, puis cliquez sur **créer** à nouveau.</span><span class="sxs-lookup"><span data-stu-id="3dcc0-103">If requested, carry out hello SMS Verification, and click **Create** again.</span></span>
   
    ![Création d’un projet](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     <span data-ttu-id="3dcc0-105">Saisissez votre nouveau **Nom du projet**, et cliquez sur **Créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="3dcc0-105">Type in your new **Project name** and click **Create project**.</span></span>
3. <span data-ttu-id="3dcc0-106">Cliquez sur hello **utilitaires et bien plus encore** puis cliquez sur **informations sur le projet**.</span><span class="sxs-lookup"><span data-stu-id="3dcc0-106">Click hello **Utilities and More** button and then click **Project Information**.</span></span> <span data-ttu-id="3dcc0-107">Prenez note de hello **numéro de projet**.</span><span class="sxs-lookup"><span data-stu-id="3dcc0-107">Make a note of hello **Project Number**.</span></span> <span data-ttu-id="3dcc0-108">Vous devez tooset cette valeur comme hello `SenderId` variable dans l’application cliente de hello.</span><span class="sxs-lookup"><span data-stu-id="3dcc0-108">You will need tooset this value as hello `SenderId` variable in hello client app.</span></span>
   
    ![Utilitaires et bien plus encore](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. <span data-ttu-id="3dcc0-110">Bonjour de projet du tableau de bord, sous **API Mobile**, cliquez sur **messagerie Cloud Google**, cliquez sur la page suivante de hello **activer l’API** et acceptez les termes de hello du service.</span><span class="sxs-lookup"><span data-stu-id="3dcc0-110">In hello project dashboard, under **Mobile APIs**, click **Google Cloud Messaging**, then on hello next page click **Enable API** and accept hello terms of service.</span></span> 
   
    ![Activation de GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Activation de GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. <span data-ttu-id="3dcc0-113">Dans le tableau de bord projet hello, cliquez sur **informations d’identification** > **Create Credential** > **clé API**.</span><span class="sxs-lookup"><span data-stu-id="3dcc0-113">In hello project dashboard, Click **Credentials** > **Create Credential** > **API Key**.</span></span> 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. <span data-ttu-id="3dcc0-114">Dans **Créer une nouvelle clé**, cliquez sur **Clé serveur**,saisissez un nom pour votre clé, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="3dcc0-114">In **Create a new key**, click **Server key**, type a name for your key, then click **Create**.</span></span>
7. <span data-ttu-id="3dcc0-115">Prenez note de hello **clé API** valeur.</span><span class="sxs-lookup"><span data-stu-id="3dcc0-115">Make a note of hello **API KEY** value.</span></span>
   
    <span data-ttu-id="3dcc0-116">Vous utiliserez cette tooenable de valeur de clé d’API Azure tooauthenticate avec GCM et envoyer des notifications push pour le compte de votre application.</span><span class="sxs-lookup"><span data-stu-id="3dcc0-116">You will use this API key value tooenable Azure tooauthenticate with GCM and send push notifications on behalf of your app.</span></span>

