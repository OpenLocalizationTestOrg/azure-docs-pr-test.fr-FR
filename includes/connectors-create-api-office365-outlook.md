#### <a name="prerequisites"></a>Composants requis
* Un compte Azure (que vous pouvez [créer gratuitement)](https://azure.microsoft.com/free)
* Un compte [Office 365](https://office365.com)  

Avant d’utiliser votre compte Office 365 dans une application logique, autoriser hello logique application tooconnect tooyour compte Office 365. Vous pouvez effectuer cela facilement au sein de votre application logique sur hello portail Azure.  

Autoriser votre logique tooconnect tooyour Office 365 Authentication à l’aide de hello comme suit :

1. Créez une application logique. Dans le concepteur hello Logic Apps, sélectionnez **Microsoft d’afficher les API managées** Bonjour liste déroulante, puis entrez « office 365 » dans la zone de recherche hello. Sélectionnez un des déclencheurs de hello ou des actions :  
    ![Étape de création de la connexion à Office 365](./media/connectors-create-api-office365-outlook/office365-sendemail.png)  
2. Si vous n’avez pas précédemment créé n’importe quel tooOffice connexions 365, vous êtes toosign demandée à l’aide de vos informations d’identification Office 365 :  
    ![étape de création de la connexion à Office 365](./media/connectors-create-api-office365-outlook/office365-signin.png)  
3. Sélectionnez **Connexion**, puis indiquez votre nom d’utilisateur et votre mot de passe. Sélectionnez **Connexion** :  
    ![Étape de création de la connexion à Office 365](./media/connectors-create-api-office365-outlook/office365-usernamepassword.png)
   
    Ces informations d’identification sont utilisée tooauthorize votre tooconnect d’application logique pour et accéder à votre compte Office 365. 
4. Avis hello connexion a été créée. Maintenant, hello autres étapes dans votre logique d’application :   
    ![étape de création de la connexion à Office 365](./media/connectors-create-api-office365-outlook/office365-sendemailproperties.png)  

