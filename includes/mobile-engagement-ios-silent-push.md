> [!IMPORTANT]
> tooreceive des Notifications Push à partir de Mobile Engagement, vous devez tooenable `Silent Remote Notifications` dans votre application. Vous devez le tableau UIBackgroundModes toohello tooadd hello valeur de la notification à distance dans votre fichier Info.plist.
> 
> 

1. Ouvrez `info.plist` fichier hello projet
2. Cliquez avec le bouton droit sur l’élément du haut dans la liste de hello hello (`Information Property List`) et ajouter une nouvelle ligne
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. Bonjour Entrez nouvelle ligne`Required background modes`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. Cliquez sur la ligne de hello tooexpand hello flèche gauche
5. Ajouter hello valeur toohello élément 0`App downloads content in response toopush notifications`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. Une fois que vous modifiez hello, info.plist hello XML doit contenir hello suivant clé et la valeur :
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. Si vous utilisez **Xcode 7+** et **iOS 9 +** :
   
   * Activer **Notifications Push** dans Cibles > Nom de cible > Fonctionnalités.

