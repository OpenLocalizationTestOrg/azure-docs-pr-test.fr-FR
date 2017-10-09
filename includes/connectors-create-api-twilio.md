### <a name="prerequisites"></a>Composants requis
* Un compte Twilio
* Un numéro de téléphone Twilio vérifié pouvant recevoir des SMS
* Un numéro de téléphone Twilio vérifié pouvant envoyer des SMS

> [!NOTE]
> Si vous utilisez un compte d’évaluation de Twilio, vous pouvez seulement envoyer des SMS trop**vérifié** les numéros de téléphone.  
> 
> 

Avant de pouvoir utiliser votre compte Twilio dans une application logique, vous devez autoriser le compte de hello logique application tooconnect tooyour Twilio. Heureusement, vous pouvez effectuer cela facilement à partir de dans votre application logique sur hello portail Azure. 

Voici votre ordinateur logique application tooconnect tooyour compte Twilio hello étapes tooauthorize :

1. Sélectionnez d’une connexion tooTwilio, dans le Concepteur d’application logique de hello, toocreate **Microsoft d’afficher les API managées** Bonjour liste déroulante, puis entrez *Twilio* dans la zone de recherche hello. Sélectionnez le déclencheur de hello ou l’action que vous apprécierez toouse :  
   ![](./media/connectors-create-api-twilio/twilio-0.png)
2. Si vous n’avez pas créé de n’importe quel tooTwilio de connexions avant, vous obtiendrez tooprovide invité à vos informations d’identification Twilio. Ces informations d’identification seront utilisée tooauthorize votre tooconnect d’application logique pour et accéder aux données de votre compte Twilio :  
   ![](./media/connectors-create-api-twilio/twilio-1.png)  
3. Vous devez hello **id de compte Twilio** et **jeton d’accès de Twilio** à partir du tableau de bord hello dans Twilio, par conséquent, connectez-vous tooyour Twilio compte maintenant toograb ces deux informations :  
   ![](./media/connectors-create-api-twilio/twilio-2.png)  
4. Les applications de Twilio et logique utilisent des noms différents tooidentify ces deux types d’informations. Voici comment vous devez mapper les boîte de dialogue applications toohello logique :![](./media/connectors-create-api-twilio/twilio-3.png)  
5. Sélectionnez hello **créer connexion** bouton :  
   ![](./media/connectors-create-api-twilio/twilio-4.png)
6. Notez hello connexion a été créée et vous êtes en train de tooproceed libre par hello autres étapes dans votre logique d’application :  
   ![](./media/connectors-create-api-twilio/twilio-5.png)

