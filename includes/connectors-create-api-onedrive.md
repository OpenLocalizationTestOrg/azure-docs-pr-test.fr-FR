#### <a name="prerequisites"></a>Composants requis
* Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)
* Un compte [OneDrive](https://www.microsoft.com/store/apps/onedrive/9wzdncrfj1p3) 

Avant de pouvoir utiliser votre compte OneDrive dans une application logique, autoriser le compte de hello logique application tooconnect tooyour OneDrive.  Vous pouvez effectuer cela facilement au sein de votre application logique sur hello portail Azure. 

Autoriser votre compte OneDrive logique application tooconnect tooyour à l’aide de hello comme suit :

1. Créez une application logique. Dans le concepteur hello Logic Apps, sélectionnez **Microsoft d’afficher les API managées** Bonjour liste déroulante, puis entrez « onedrive » dans la zone de recherche hello. Sélectionnez un des déclencheurs de hello ou des actions :  
   ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. Si vous n’avez pas précédemment créé tooOneDrive de toutes les connexions, vous êtes toosign demandée à l’aide de vos informations d’identification OneDrive :  
   ![](./media/connectors-create-api-onedrive/onedrive-2.png)
3. Sélectionnez **Connexion**, puis indiquez votre nom d’utilisateur et votre mot de passe. Sélectionnez **Connexion** :  
   ![](./media/connectors-create-api-onedrive/onedrive-3.png)   
   
    Ces informations d’identification sont utilisée tooauthorize votre tooconnect d’application logique pour et accéder aux données hello dans votre compte OneDrive. 
4. Sélectionnez **Oui** tooauthorize hello toouse d’application logique de votre compte OneDrive :  
   ![](./media/connectors-create-api-onedrive/onedrive-4.png)   
5. Avis hello connexion a été créée. Maintenant, hello autres étapes dans votre logique d’application :  
   ![](./media/connectors-create-api-onedrive/onedrive-5.png)

