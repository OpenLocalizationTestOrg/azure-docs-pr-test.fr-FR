### <a name="prerequisites"></a>Composants requis
Vous devez disposer d’un compte [Service Bus](https://azure.microsoft.com/services/service-bus/).  

Avant de pouvoir utiliser votre compte Azure Service Bus dans une application logique, vous devez autoriser le compte du service bus tooyour hello logique applications tooconnect. Heureusement, vous pouvez effectuer cela facilement à partir de dans votre application logique sur hello portail Azure.  

Voici votre ordinateur logique application tooconnect tooyour compte de Service Bus hello étapes tooauthorize :  

1. Sélectionnez d’un Bus, de tooService connexion dans le Concepteur d’application logique de hello, toocreate **Microsoft d’afficher les API managées** dans la liste déroulante de hello. Puis entrez **service bus** dans la zone de recherche hello. Sélectionnez le déclencheur de hello ou l’action que vous souhaitez toouse.  
    ![Image de connexion à Service Bus 1](./media/connectors-create-api-servicebus/servicebus-1.png)  
2. Si vous n’avez pas créé de n’importe quel tooService connexions Bus avant, vous serez invité à tooprovide vos informations d’identification de Service Bus. Ces informations d’identification sont utilisée tooauthorize votre tooand de tooconnect logique application accéder aux données de votre compte Service Bus. connecteur de Service Bus Hello doit la chaîne de connexion hello pour l’espace de noms Service Bus hello. Il nécessite également des autorisations de **gestion**. Un tooknow recommandée si votre chaîne de connexion est pour l’espace de noms hello ou une entité spécifique est si elle contient hello `EntityPath` paramètre. Dans ce cas, il n’est pas chaîne de connexion adéquate hello pour une application logique.  
    ![Chaîne de connexion à Service Bus](./media/connectors-create-api-servicebus/connectionstring.png)
3. Une fois que vous avez reçu la chaîne de connexion hello pour l’espace de noms hello, vous pouvez l’utiliser pour hello connexion API dans les applications de la logique.  
    ![Image de connexion à Service Bus 2](./media/connectors-create-api-servicebus/servicebus-2.png)  
4. Notez hello connexion a été créée, et vous êtes en train de tooproceed libre par hello autres étapes dans votre application logique.  
    ![Image de connexion à Service Bus 3](./media/connectors-create-api-servicebus/servicebus-3.png)   

