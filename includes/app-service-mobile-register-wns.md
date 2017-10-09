
1. Dans l’Explorateur de solutions Visual Studio, cliquez sur le projet d’application Windows Store hello, puis cliquez sur **magasin** > **associer application hello magasin**.

    ![Associer une application au Windows Store](./media/app-service-mobile-register-wns/notification-hub-associate-win8-app.png)
2. Dans l’Assistant de hello, cliquez sur **suivant**et connectez-vous avec votre compte Microsoft. Tapez un nom pour l’application dans **Réserver un nouveau nom d’application**, puis cliquez sur **Réserver**.
3. Une fois l’inscription d’une application hello nouveau nom d’application a été créé correctement, sélectionnez hello, cliquez sur **suivant**, puis cliquez sur **associer**. Cela ajoute le manifeste d’application d’enregistrement d’informations toohello hello requis du Windows Store.
4. Répétez les étapes 1 et 3 pour le projet d’application Windows Phone Store hello à l’aide de hello même enregistrement que vous avez créé précédemment pour l’application du Windows Store hello.  
5. Parcourir toohello [centre de développement Windows](https://dev.windows.com/en-us/overview)et connectez-vous avec votre compte Microsoft. Cliquez sur nouvelle inscription d’application hello dans **mes applications**, puis développez **Services** > **des notifications Push**.
6. Sur hello **des notifications Push** , cliquez sur **site des Services Live** sous **Services de notifications Push Windows (WNS) et Microsoft Azure Mobile Apps**. Prenez note des valeurs hello Hello **SID du Package** et hello *actuel* valeur **Secret d’Application**. 

    ![Paramètre d’application dans le centre de développement hello](./media/app-service-mobile-register-wns/mobile-services-win8-app-push-auth.png)

   > [!IMPORTANT]
   > secret d’application Hello et le SID du package sont des informations d’identification de sécurité importantes. Ne partagez pas ces valeurs avec quiconque et ne les distribuez pas avec votre application.
   >
   >
