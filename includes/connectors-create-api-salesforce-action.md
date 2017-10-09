Maintenant que vous avez ajouté une condition, son heure de toodo quelque chose intéressante avec des données hello sont générées par le déclencheur de hello. Suivez ces hello de tooadd étapes **Salesforce - obtention de l’objet** action. Cette opération obtiendra-t-elle les données de hello chaque fois qu’un nouveau prospect est créé. Vous allez également ajouter une deuxième action qui utilise les données hello de hello Salesforce - Get une toosend d’action objet un message électronique à l’aide du connecteur de hello Office 365.  

tooconfigure hello cette action, vous devez hello tooprovide informations suivantes. Vous remarquerez qu’il s’agit de données simple toouse générées par le déclencheur de hello en tant qu’entrée pour certaines des propriétés hello pour le nouveau fichier de hello :

| Propriété Créer un fichier | Description |
| --- | --- |
| Type d'objet |Il s’agit de type hello d’objet Salesforce que vous intéressez. Par exemple Prospect, Client, etc. |
| ID objet |Représente un identificateur d’objet de hello. |

1. Sélectionnez le lien **Ajouter une action** . Cette zone de recherche hello s’ouvre dans laquelle vous pouvez rechercher n’importe quelle action vous aimeriez tootake. Pour cet exemple, les actions de Salesforce nous intéressent.      
   ![Image d’action Salesforce 1](./media/connectors-create-api-salesforce/action-1.png)  
2. Entrez *salesforce* toosearch pour toosalesforce connexes d’actions.
3. Sélectionnez **Salesforce - obtention de l’objet** comme hello tootake d’action.   **Remarque**: vous est demandée tooauthorize votre tooaccess d’application logique votre Salesforce compte si vous le n'avez pas fait précédemment.    
   ![Image d’action Salesforce 2](./media/connectors-create-api-salesforce/action-2.png)    
4. Hello **obtention de l’objet** contrôle s’ouvre.  
5. Sélectionnez *entraîner* en tant que type d’objet hello.
6. Sélectionnez hello **ID d’objet** contrôle.
7. Sélectionnez **...**  liste de hello tooexpand de jetons qui peut être utilisé comme entrée pour les actions.       
   ![Image d’action Salesforce 3](./media/connectors-create-api-salesforce/action-3.png)    
8. Le contrôle Sélectionner **ID de prospect** s’ouvre.   
   ![Image d’action Salesforce 4](./media/connectors-create-api-salesforce/action-4.png)     
9. Notez que ce jeton d’ID prospect hello est désormais hello contrôle ID d’objet, indiquant que hello Get objet action permet de rechercher un message avec un ID qui est l’ID de responsable toohello égale de prospect qui a déclenché cette application logique.  
   ![Image d’action Salesforce 5](./media/connectors-create-api-salesforce/action-5.png)  
10. Enregistrez votre travail. Par conséquent, vous avez ajouté application logique de hello Get objet action tooyour. Votre contrôle Obtenir un objet doit ressembler à ceci :     
    ![Image d’action Salesforce 6](./media/connectors-create-api-salesforce/action-6.png)  

Maintenant que vous avez ajouté une action de tooget un prospect, vous souhaiterez toodo quelque chose intéressante avec tête de hello nouvellement créé. Dans une entreprise, vous pouvez vouloir toosend un toonotify par courrier électronique une liste de distribution qu’un nouveau prospect a été créé. Nous allons utiliser hello Office 365 connecteur toosend un message électronique avec certaines des informations pertinentes relatives hello hello responsable d’objet dans Salesforce.  

1. Sélectionnez **ajouter une action** puis entrez *e-mail* dans le contrôle de recherche hello. Cela permet de filtrer hello actions toothose toosending connexe et la réception de courrier électronique.  
2. Sélectionnez hello **Outlook Office 365 - envoyer un e-mail** élément de liste. Si vous n’avez pas déjà créé un *connexion* tooyour compte Office 365, vous allez être invité à tooenter votre toocreate d’informations d’identification Office 365 informatique maintenant. Une fois que vous avez terminé, hello **envoyer un courrier électronique** contrôle s’ouvre.        
   ![Image d’action Salesforce 7](./media/connectors-create-api-salesforce/action-7.png)  
3. Entrez hello adresse de messagerie que vous aimeriez hello de tooin de messagerie toosend **à** contrôle.
4. Bonjour **sujet** contrôler, entrez *nouveau prospect créé* - puis hello *société* jeton. Cette action affiche hello *société* champ prospect hello créée dans Salesforce.  
5. Bonjour **corps** (contrôle), vous pouvez sélectionner un des jetons hello de nouvel objet de prospect hello et vous pouvez également saisir un texte toodisplay dans le corps de hello du hello par courrier électronique. Voici un exemple :  
   ![Image d’action Salesforce 8](./media/connectors-create-api-salesforce/action-8.png)   
6. Enregistrez votre flux de travail.  

Vous avez terminé. Votre application logique est maintenant terminée.  

Vous pouvez maintenant tester votre application logique : dans Salesforce, créez un nouveau prospect qui répond à la condition hello créée.  Si vous avez suivi cette procédure pas à pas en intégralité, créez simplement un prospect avec une adresse de messagerie qui contient *amazon.com* . Après quelques secondes votre application logique doit être déclenchée, et les résultats de hello peuvent sembler similaires toothis :  
![Image d’action Salesforce 9](./media/connectors-create-api-salesforce/action-9.png)  

