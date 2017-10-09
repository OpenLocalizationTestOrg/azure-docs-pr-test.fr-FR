

1. Sur votre Mac, démarrez **Trousseau d’accès**. Dans hello gauche barre de navigation, sous **catégorie**, ouvrez **mes certificats**. Trouver le certificat SSL de hello que vous avez téléchargé dans la section précédente de hello et divulguer son contenu. Sélectionnez hello uniquement le certificat (ne sélectionnez pas de clé privée de hello), et [exportez-le](https://support.apple.com/kb/PH20122?locale=en_US).
2. Bonjour [portail Azure](https://portal.azure.com/), cliquez sur **parcourir tous les** > **des Services d’application**, puis cliquez sur votre serveur d’applications mobiles principal. Sous **Paramètres**, cliquez sur **App Service Push (Notification Push App Service)**, puis sur le nom de votre hub de notification. Accédez trop**Services de notifications Push Apple** > **télécharger un certificat**. Charger le fichier de .p12 hello, en sélectionnant hello correct **Mode** (selon si votre client SSL de certificat précédemment est production ou bac à sable). Enregistrez les modifications.

Votre service est maintenant configuré toowork avec les notifications push sur iOS.

[1]: ./media/app-service-mobile-apns-configure-push/mobile-push-notification-hub.png
