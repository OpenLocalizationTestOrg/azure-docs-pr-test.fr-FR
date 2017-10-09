
1. <span data-ttu-id="20e82-101">Bonjour, vue de la Solution (ou **l’Explorateur de solutions** dans Visual Studio), avec le bouton hello **composants** dossier, cliquez sur **obtenir plusieurs composants...** , recherchez hello **Client de messagerie Cloud Google** composant et l’ajouter toohello projet.</span><span class="sxs-lookup"><span data-stu-id="20e82-101">In hello Solution view (or **Solution Explorer** in Visual Studio), right-click hello **Components** folder, click  **Get More Components...**, search for hello **Google Cloud Messaging Client** component and add it toohello project.</span></span>
2. <span data-ttu-id="20e82-102">Ouvrez le fichier de projet ToDoActivity.cs hello et ajoutez hello qui suit à l’aide de la classe toohello d’instruction :</span><span class="sxs-lookup"><span data-stu-id="20e82-102">Open hello ToDoActivity.cs project file and add hello following using statement toohello class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="20e82-103">Bonjour **ToDoActivity** de classe, ajoutez hello suivant le nouveau code :</span><span class="sxs-lookup"><span data-stu-id="20e82-103">In hello **ToDoActivity** class, add hello following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return hello current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return hello Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="20e82-104">Cela vous permet de tooaccess instance de client mobile hello à partir de processus du service Gestionnaire de push hello.</span><span class="sxs-lookup"><span data-stu-id="20e82-104">This enables you tooaccess hello mobile client instance from hello push handler service process.</span></span>
4. <span data-ttu-id="20e82-105">Ajouter hello suivant code toohello **OnCreate** méthode, après hello **MobileServiceClient** est créé :</span><span class="sxs-lookup"><span data-stu-id="20e82-105">Add hello following code toohello **OnCreate** method, after hello **MobileServiceClient** is created:</span></span>
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="20e82-106">Votre **ToDoActivity** est maintenant prêt pour l'ajout de notifications push.</span><span class="sxs-lookup"><span data-stu-id="20e82-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

