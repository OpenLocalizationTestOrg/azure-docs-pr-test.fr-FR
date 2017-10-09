1. Connectez-vous à l’adresse hello [Azure Portal].
2. Cliquez sur **+NOUVEAU** > **Web + Mobile** > **Application mobile**, puis indiquez le nom de votre serveur principal Mobile App.
3. Pourquoi **groupe de ressources**, sélectionnez un groupe de ressources existant ou créez-en un nouveau (à l’aide de hello même nom que votre application). 
   
    Sélectionnez un autre plan App Service ou créez-en un. Pour plus d’informations sur les plans de Services d’application et comment toocreate un nouveau plan dans différents tarifs de couche et dans l’emplacement souhaité, consultez [vue d’ensemble approfondie des plans de Service d’applications Azure](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Pourquoi **plan App Service**, plan par défaut de hello (Bonjour [niveau Standard](https://azure.microsoft.com/pricing/details/app-service/)) est sélectionné. Vous pouvez sélectionner un autre plan ou en [créer un](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). les paramètres du plan App Service Hello déterminent hello [emplacement, fonctionnalités, de coût et des ressources de calcul](https://azure.microsoft.com/pricing/details/app-service/) associé à votre application. 
   
    Après avoir choisi le plan de hello, cliquez sur **créer**. Cela crée le principal de l’application Mobile hello. 
5. Bonjour **paramètres** panneau pour hello nouveau principal de l’application Mobile, cliquez sur **démarrage rapide** > votre plateforme d’application client > **se connecter à une base de données**. 
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-data-connection.png)
6. Bonjour **ajouter une connexion de données** panneau, cliquez sur **base de données SQL** > **créer une base de données**, base de données de type hello **nom**, Choisissez un niveau tarifaire, puis cliquez sur **Server**.  Vous pouvez réutiliser cette nouvelle base de données. Si vous disposez déjà d’une base de données Bonjour même emplacement, vous pouvez à la place choisir **utiliser une base de données**. Hello l’utilisation d’une base de données dans un autre emplacement n’est pas recommandée en raison des coûts de toobandwidth et une latence plus élevée.
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-db.png)
7. Bonjour **nouveau serveur** panneau, tapez un nom de serveur unique Bonjour **nom du serveur** champ, fournir une connexion et un mot de passe, vérifiez **server de tooaccess autoriser les services azure**, puis cliquez sur **OK**. Cela crée la nouvelle base de données hello.
8. Dans hello **ajouter une connexion de données** panneau, cliquez sur **chaîne de connexion**, tapez les valeurs de connexion et mot de passe hello pour votre base de données, puis cliquez sur **OK**. Attendez quelques minutes pour hello toobe de base de données déployée avec succès avant de continuer.

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/
