### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>Grant Mobile Engagement accès tooyour clé API GCM
tooallow Mobile Engagement toosend des notifications push à votre place, vous devez toogrant il tooyour clé API d’accès. Pour cela, en configurant et entrer votre clé dans le portail Mobile Engagement de hello.

1. À partir de votre portail classique Azure, vérifiez dans l’application hello nous à utiliser pour ce projet, puis cliquez sur hello **Engage** bouton bas hello :
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. Puis cliquez sur hello **paramètres** -> **le Push natif** section tooenter votre clé GCM :
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. Cliquez sur hello **modifier** icône devant **clé API** Bonjour **GCM paramètres** section comme indiqué ci-dessous :
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. Dans la fenêtre contextuelle hello, collez hello clé du serveur GCM vous avez obtenus avant et puis cliquez sur **Ok**.
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <a id="send"></a>Envoi d’une application tooyour de notification
Nous allons maintenant créer une campagne de notification push simple qui envoie une application tooour de notification push.

1. Accédez toohello **atteindre** onglet dans votre portail Mobile Engagement.
2. Cliquez sur **nouvelle annonce** toocreate votre campagne de notification push.
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. Vous pouvez configurer hello premier champ de votre campagne via hello comme suit :
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    a. Nommez votre campagne.
   
    b. Sélectionnez hello **type de remise** en tant que *notification système -> Simple*: il s’agit type de notification push Android simple hello qui propose un titre et une petite ligne de texte.
   
    c. Sélectionnez **heure de remise** en tant que *tout moment* tooallow hello application tooreceive une notification si l’application hello est démarrée ou non.
   
    d. Bonjour de type texte hello notification **titre** qui sera en gras dans les push hello.
   
    e. Tapez ensuite votre **message**
4. Faites défiler vers le bas et hello **contenu** section, sélectionnez **Notification uniquement**.
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. Vous avez terminé possible de campagne paramètre hello plus simple. Maintenant défiler à nouveau vers le bas et cliquez sur hello **créer** bouton toosave votre campagne.
6. Dernière étape : cliquez sur **activer** tooactivate vos notifications push de toosend campagne.
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

