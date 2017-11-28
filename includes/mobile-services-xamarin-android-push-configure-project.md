
1. <span data-ttu-id="4cedd-101">Dans la vue Solution (ou dans l’**Explorateur de solutions** dans Visual Studio), cliquez avec le bouton droit sur le dossier **Components**, cliquez sur **Get More Components...**, recherchez le composant **Google Cloud Messaging Client**, puis ajoutez-le au projet.</span><span class="sxs-lookup"><span data-stu-id="4cedd-101">In the Solution view (or **Solution Explorer** in Visual Studio), right-click the **Components** folder, click  **Get More Components...**, search for the **Google Cloud Messaging Client** component and add it to the project.</span></span>
2. <span data-ttu-id="4cedd-102">Ouvrez le fichier projet ToDoActivity.css et ajoutez l'instruction using suivante à la classe :</span><span class="sxs-lookup"><span data-stu-id="4cedd-102">Open the ToDoActivity.cs project file and add the following using statement to the class:</span></span>
   
        using Gcm.Client;
3. <span data-ttu-id="4cedd-103">Dans la classe **ToDoActivity** , ajoutez le nouveau code suivant :</span><span class="sxs-lookup"><span data-stu-id="4cedd-103">In the **ToDoActivity** class, add the following new code:</span></span> 
   
        // Create a new instance field for this activity.
        static ToDoActivity instance = new ToDoActivity();
   
        // Return the current activity instance.
        public static ToDoActivity CurrentActivity
        {
            get
            {
                return instance;
            }
        }
        // Return the Mobile Services client.
        public MobileServiceClient CurrentClient
        {
            get
            {
                return client;
            }
        }
   
    <span data-ttu-id="4cedd-104">Vous pouvez ainsi accéder à l’instance du client mobile depuis le processus de service de gestionnaire push.</span><span class="sxs-lookup"><span data-stu-id="4cedd-104">This enables you to access the mobile client instance from the push handler service process.</span></span>
4. <span data-ttu-id="4cedd-105">Ajoutez le code ci-après à la méthode **OnCreate** après la création de **MobileServiceClient** :</span><span class="sxs-lookup"><span data-stu-id="4cedd-105">Add the following code to the **OnCreate** method, after the **MobileServiceClient** is created:</span></span>
   
       // Set the current instance of TodoActivity.
       instance = this;
   
       // Make sure the GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register the app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

<span data-ttu-id="4cedd-106">Votre **ToDoActivity** est maintenant prêt pour l'ajout de notifications push.</span><span class="sxs-lookup"><span data-stu-id="4cedd-106">Your **ToDoActivity** is now prepared for adding push notifications.</span></span>

