
1. Bonjour, vue de la Solution (ou **l’Explorateur de solutions** dans Visual Studio), avec le bouton hello **composants** dossier, cliquez sur **obtenir plusieurs composants...** , recherchez hello **Client de messagerie Cloud Google** composant et l’ajouter toohello projet.
2. Ouvrez le fichier de projet ToDoActivity.cs hello et ajoutez hello qui suit à l’aide de la classe toohello d’instruction :
   
        using Gcm.Client;
3. Bonjour **ToDoActivity** de classe, ajoutez hello suivant le nouveau code : 
   
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
   
    Cela vous permet de tooaccess instance de client mobile hello à partir de processus du service Gestionnaire de push hello.
4. Ajouter hello suivant code toohello **OnCreate** méthode, après hello **MobileServiceClient** est créé :
   
       // Set hello current instance of TodoActivity.
       instance = this;
   
       // Make sure hello GCM client is set up correctly.
       GcmClient.CheckDevice(this);
       GcmClient.CheckManifest(this);
   
       // Register hello app for push notifications.
       GcmClient.Register(this, ToDoBroadcastReceiver.senderIDs);

Votre **ToDoActivity** est maintenant prêt pour l'ajout de notifications push.

