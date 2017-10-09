### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a>Accorder l’accès tooyour pousser le certificat tooMobile Engagement
tooallow Mobile Engagement toosend des Notifications Push à votre place, vous devez toogrant il tooyour certificat d’accès. Cela est fait en configurant et en entrant votre certificat dans le portail Mobile Engagement de hello. Assurez-vous d'obtenir votre certificat .p12 comme expliqué dans la [documentation d'Apple](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

1. Accédez portail Mobile Engagement de tooyour. Vérifiez que vous êtes dans hello correct, puis cliquez sur hello **Engage** bouton bas hello :
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. Cliquez sur hello **paramètres** page de votre portail du projet. À partir de là, cliquez sur hello **le Push natif** section tooupload votre certificat p12 :
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. Sélectionnez votre p12, téléchargez-le et tapez votre mot de passe :
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <a id="send"></a>Envoi d’une application tooyour de notification
Nous allons maintenant créer une campagne de Notification Push simple qui envoie une application de tooour par émission de données :

1. Accédez toohello **atteindre** onglet dans votre portail Mobile Engagement.
2. Cliquez sur **nouvelle annonce** toocreate votre campagne push
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. Le programme d’installation hello premiers champs de votre campagne :
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * Entrez un **nom** pour votre campagne. 
   * Sélectionnez hello **heure de remise** en tant que **hors de l’application uniquement**: il s’agit hello Apple push notification type simple qui propose du texte.
   * Dans le texte de notification hello, tapez Bonjour première **titre** qui sera hello première ligne de commande de hello.
   * Puis tapez votre **Message** qui sera la deuxième ligne de hello
4. Faites défiler et Bonjour section de contenu, sélectionnez **Notification uniquement**
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. Vous avez terminé la campagne de paramètre hello plus simple. Maintenant faites défiler la liste et cliquez sur **créer** bouton toosave votre campagne de notification push. 
6. -Cliquez sur **activer** toosend de notifications push. 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. Vous serez en mesure de recevoir une notification de hello sur votre appareil iOS dans le centre de notification hello hello suivante :
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. Si vous avez une Apple Watch associé à cet appareil iOS vous voyez ensuite hello notification sur votre Apple Watch :
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

