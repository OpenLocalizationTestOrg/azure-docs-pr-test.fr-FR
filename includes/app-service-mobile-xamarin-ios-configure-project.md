#### <a name="configure-hello-ios-project-in-xamarin-studio"></a>Configurer le projet d’iOS hello dans Xamarin Studio
1. Dans Xamarin.Studio, ouvrez **Info.plist**et la mise à jour hello **identificateur de lot** avec hello regrouper ID que vous avez créé précédemment avec votre nouvel ID d’application.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. Faites défiler la liste trop**Modes d’arrière-plan**. Sélectionnez hello **activer les Modes d’arrière-plan** boîte et hello **des notifications à distance** boîte.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. Double-cliquez sur votre projet dans tooopen du Panneau de configuration de Solution hello **Options du projet**.
4. Sous **générer**, choisissez **signature d’offre groupée iOS**et sélectionnez hello identité correspondante et profil de configuration vous venez de définir pour ce projet.

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   Cela garantit que ce projet hello utilise le nouveau profil de hello pour la signature de code. Hello officiel Xamarin unité documentation de configuration, consultez [Xamarin configuration].

#### <a name="configure-hello-ios-project-in-visual-studio"></a>Configurer le projet d’iOS hello dans Visual Studio
1. Dans Visual Studio, cliquez sur le projet de hello, puis cliquez sur **propriétés**.
2. Dans les pages de propriétés de hello, cliquez sur hello **iOS Application** onglet et mise à jour hello **identificateur** avec l’ID de hello que vous avez créé précédemment.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. Bonjour **signature d’offre groupée iOS** sous l’onglet identité correspondante de sélection hello et de configuration de profil vous venez de définir pour ce projet.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    Cela garantit que ce projet hello utilise le nouveau profil de hello pour la signature de code. Hello officiel Xamarin unité documentation de configuration, consultez [Xamarin configuration].
4. Double-cliquez sur le fichier Info.plist tooopen, puis activez **RemoteNotifications** sous **Modes d’arrière-plan**.

[Xamarin configuration]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
