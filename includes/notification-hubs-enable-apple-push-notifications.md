

## <a name="generate-hello-certificate-signing-request-file"></a>Générer le fichier de demande de signature de certificat hello
Hello Apple Push Notification Service (APNS) utilise des certificats tooauthenticate vos notifications push. Suivez ces toosend de certificat instructions toocreate hello push nécessaires et recevoir des notifications. Pour plus d’informations sur ces concepts, consultez officielle de hello [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.

Générer le fichier de demande de signature de certificat (CSR) hello, qui est utilisé par Apple toogenerate un certificat signé par émission de données.

1. Sur votre Mac, exécutez hello outil de trousseau d’accès. Il peut être ouverte à partir de hello **utilitaires** dossier ou hello **autres** dossier sur la zone de lancement hello.
2. Cliquez sur **Trousseaux d'accès**, développez **Assistant de certification**, puis cliquez sur **Demander un certificat à une autorité de certification**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. Sélectionnez votre **adresse de messagerie utilisateur** et **nom commun** , assurez-vous que **enregistré toodisk** est sélectionné, puis cliquez sur **continuer**. Laissez hello **adresse de messagerie d’autorité de certification** champ vide car il n’est pas requis.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. Tapez un nom pour le fichier de demande de signature de certificat (CSR) hello dans **enregistrer en tant que**, sélectionnez l’emplacement de hello dans **où**, puis cliquez sur **enregistrer**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      Ce fichier de signature de certificat hello enregistre dans l’emplacement de hello sélectionné ; emplacement par défaut de Hello est hello bureau. N’oubliez pas d’emplacement de hello choisi pour ce fichier.

Ensuite, vous l’inscrivez auprès d’Apple, activer les notifications push et télécharger cette toocreate de signature de certificat exporté un certificat push.

## <a name="register-your-app-for-push-notifications"></a>Inscription de votre application pour les notifications Push
toobe toosend en mesure de push notifications tooan iOS application, vous devez inscrire votre application avec Apple et également s’inscrire pour des notifications push.  

1. Si vous n’avez pas encore inscrit votre application, accédez à toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> au hello Apple Developer Center, ouverture de session avec votre ID Apple, cliquez sur **identificateurs**, puis cliquez sur **ID d’application** et enfin cliquez sur hello  **+**  tooregister une nouvelle application de connexion.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. Mettre à jour hello suivant trois champs pour votre nouvelle application, puis cliquez sur **continuer**:
   
   * **Nom**: tapez un nom descriptif pour votre application Bonjour **nom** champ hello **Description de l’ID d’application** section.
   * **Identificateur d’offres groupées**: sous hello **ID d’application explicite** section, entrez un **identificateur de lot** sous forme de hello `<Organization Identifier>.<Product Name>` comme indiqué dans hello [Distribution d’applications Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8). Hello *identifiant d’organisation* et *Product Name* vous utilisez doit correspondre à l’identificateur de l’organisation hello et nom de produit à utiliser lorsque vous créez votre projet XCode. Dans screeshot hello ci-dessous *NotificationHubs* est utilisé comme un identificateur de l’organisation et *GetStarted* est utilisé comme nom de produit hello. S’assurer que cela correspond aux valeurs hello que vous utiliserez dans votre projet XCode permettra de vous toouse hello correct profil de publication avec XCode. 
   * **Notifications push**: vérification hello **des Notifications Push** option Bonjour **des Services d’application** section.
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      Cette opération génère votre ID d’application et vous demande des informations de hello tooconfirm. Cliquez sur **inscrire** tooconfirm hello nouvel ID d’application.
     
      Une fois que vous cliquez sur **inscrire**, vous verrez hello **inscription Terminer** écran, comme indiqué ci-dessous. Cliquez sur **Done**.
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. Bonjour centre de développement, sous l’ID d’application, recherchez hello ID d’application que vous venez de créer et cliquez sur sa ligne.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      Vous pouvez afficher les détails de l’application hello en cliquant sur l’ID de l’application hello. Cliquez sur hello **modifier** bouton bas hello.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. Faites défiler bas toohello d’écran hello et cliquez sur hello **créer un certificat...**  sous la section de hello **développement le certificat SSL Push**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      Cela permet d’afficher l’assistant « Ajouter iOS de certificat » hello.
   
   > [!NOTE]
   > Ce didacticiel utilise un certificat de développement. Hello même processus est utilisé lors de l’inscription d’un certificat de production. Assurez-vous simplement que vous utilisez hello même type de certificat lors de l’envoi des notifications.
   > 
   > 
3. Cliquez sur **choisir un fichier**, rechercher l’emplacement de toohello où vous avez enregistré le fichier CSR hello que vous avez créé dans la première tâche de hello, puis cliquez sur **générer**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. Une fois le certificat de hello est créé par le portail de hello, cliquez sur hello **télécharger** , puis cliquez sur **fait**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      Il télécharge hello certificat et l’enregistre tooyour ordinateur dans le dossier Téléchargements.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > Par défaut, hello téléchargé un certificat de développement se nomme **aps_development.cer**.
   > 
   > 
5. Double-cliquez sur : certificat push téléchargé hello **aps_development.cer**.
   
      Cette commande installe un nouveau certificat hello dans hello trousseau, comme indiqué ci-dessous :
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > nom Hello dans votre certificat peut être différent, mais il est précédé de **Apple développement iOS Services Push :**.
   > 
   > 
6. Dans le trousseau d’accès, avec le bouton droit hello nouveau poussée du certificat que vous avez créé dans hello **certificats** catégorie. Cliquez sur **exporter**, nommez le fichier de hello, sélectionnez hello **.p12** mettre en forme, puis cliquez sur **enregistrer**.
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    Rendre une note hello du nom de fichier et l’emplacement du certificat exporté .p12 de hello. Il s’agit de l’authentification tooenable utilisé avec APNS.
   
   > [!NOTE]
   > Ce didacticiel permet de créer un fichier QuickStart.p12. Il est possible que le nom de votre fichier et son emplacement sont différents.
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a>Créer un profil de configuration pour l’application hello
1. Dans hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, sélectionnez **profils de configuration**, sélectionnez **tous les**, puis cliquez sur hello  **+**  bouton toocreate un nouveau profil. Cette opération lance hello **ajouter Provisiong profil iOS** Assistant
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. Sélectionnez **iOS le développement d’applications** sous **développement** en tant que type de profil hello provisiong, puis cliquez sur **continuer**. 
3. Ensuite, sélectionnez ID d’application hello vous venez de créer à partir de hello **ID d’application** liste déroulante, puis cliquez sur **continuer**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. Bonjour **sélectionner les certificats** écran, sélectionnez votre certificat habituelles de développement utilisé pour la signature de code, puis cliquez sur **continuer**. Il ne s’agit pas de certificat de push de hello que vous venez de créer.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. Ensuite, sélectionnez hello **périphériques** toouse pour le test, puis cliquez sur **continuer**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. Enfin, choisissez un nom pour le profil hello dans **nom du profil**, cliquez sur **générer**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. Lors de la création de nouveau profil de configuration de hello cliquez sur toodownload et installer sur votre ordinateur de développement Xcode. Cliquez ensuite sur **Terminé**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
