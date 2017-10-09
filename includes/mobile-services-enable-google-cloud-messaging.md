
1. Accédez toohello [Google Cloud Console](https://console.developers.google.com/project), connectez-vous avec vos informations d’identification du compte Google. 
2. Cliquez sur **Créer un projet**, saisissez un nom de projet, puis cliquez sur **Créer**. Le cas échéant, effectuer hello vérification par SMS, puis cliquez sur **créer** à nouveau.
   
    ![Création d’un projet](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     Saisissez votre nouveau **Nom du projet**, et cliquez sur **Créer un projet**.
3. Cliquez sur hello **utilitaires et bien plus encore** puis cliquez sur **informations sur le projet**. Prenez note de hello **numéro de projet**. Vous devez tooset cette valeur comme hello `SenderId` variable dans l’application cliente de hello.
   
    ![Utilitaires et bien plus encore](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. Bonjour de projet du tableau de bord, sous **API Mobile**, cliquez sur **messagerie Cloud Google**, cliquez sur la page suivante de hello **activer l’API** et acceptez les termes de hello du service. 
   
    ![Activation de GCM](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![Activation de GCM](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. Dans le tableau de bord projet hello, cliquez sur **informations d’identification** > **Create Credential** > **clé API**. 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. Dans **Créer une nouvelle clé**, cliquez sur **Clé serveur**,saisissez un nom pour votre clé, puis cliquez sur **Créer**.
7. Prenez note de hello **clé API** valeur.
   
    Vous utiliserez cette tooenable de valeur de clé d’API Azure tooauthenticate avec GCM et envoyer des notifications push pour le compte de votre application.

