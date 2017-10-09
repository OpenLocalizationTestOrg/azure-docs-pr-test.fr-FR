Maintenant que vous avez ajouté un déclencheur, son heure de toodo quelque chose intéressante avec des données hello sont générées par le déclencheur de hello. Suivez ces hello de tooadd étapes **SharePoint Online - créer le fichier** action. Cette action créera un fichier dans SharePoint Online chaque heure hello nouvel élément déclencheur se déclenche. 

tooconfigure hello cette action, vous devez hello tooprovide informations suivantes. Vous spécifiez ces informations, vous remarquerez qu’il s’agit de données simple toouse générées par le déclencheur de hello en tant qu’entrée pour certaines des propriétés hello pour le nouveau fichier de hello :

| Propriété Créer un fichier | Description |
| --- | --- |
| URL du site |Il s’agit d’URL de hello du site SharePoint Online de hello où vous voulez que toocreate hello nouveau fichier. Sélectionnez site de hello dans liste hello présentée. |
| Chemin d’accès du dossier |Cela est hello dossier (à l’URL du Site sélectionné à l’étape précédente de hello de hello) où le nouveau fichier de hello sera placé. Recherchez et sélectionnez le dossier de hello. |
| Nom de fichier |Il s’agit de nom hello du fichier hello en cours de création. |
| le contenu d’un fichier ; |contenu de Hello toohello fichier sera écrit. |

1. Sélectionnez **+ nouvelle étape** action de hello tooadd.  
   ![Image d’action en ligne SharePoint 1](./media/connectors-create-api-sharepointonline/action-1.png)  
2. Sélectionnez hello **ajouter une action** lien. Cette zone de recherche hello s’ouvre dans laquelle vous pouvez rechercher n’importe quelle action vous aimeriez tootake. Pour cet exemple, les actions SharePoint nous intéressent.    
   ![Image d’action en ligne SharePoint 2](./media/connectors-create-api-sharepointonline/action-2.png)    
3. Entrez *sharepoint* toosearch pour tooSharePoint connexes d’actions.
4. Sélectionnez **SharePoint Online - créer le fichier** comme hello tootake d’action.   **Remarque**: vous est demandée tooauthorize votre tooaccess d’application logique de compte SharePoint si vous n’avez pas précédemment créé une tooSharePoint de connexion en ligne.    
   ![Image d’action en ligne SharePoint 3](./media/connectors-create-api-sharepointonline/action-3.png)    
5. Hello **créer un fichier** contrôle s’ouvre.   
   ![Image d’action en ligne SharePoint 4](./media/connectors-create-api-sharepointonline/action-4.png)     
6. Sélectionnez **URL du Site** et parcourir toofind hello site où vous souhaitez que le fichier de hello toocreate.     
   ![Image d’action en ligne SharePoint 5](./media/connectors-create-api-sharepointonline/action-5.png)  
7. Sélectionnez **chemin d’accès du dossier** et parcourir un dossier hello toofind où seront placés les fichiers de nouveau hello.  
   ![Image d’action en ligne SharePoint 6](./media/connectors-create-api-sharepointonline/action-6.png)  
8. Sélectionnez hello **nom de fichier** contrôler et entrez hello nom du fichier de hello souhaité toocreate. Ici, vous pouvez soit entrer les nom de fichier hello directement, ou vous pouvez utiliser une des propriétés hello déclencheur hello que vous avez créé précédemment. Pour cela en sélectionnant Propriétés dans la liste des hello **sorties à partir de la création d’un nouvel élément**. Cette liste est le seul affichage après avoir sélectionné hello **nom de fichier** contrôle. Dans cette procédure pas à pas, j’ai sélectionné ID (ID hello du nouvel élément de liste hello) en tant que nom hello du fichier hello en hello **SharePoint Online - créer le fichier** action.    
   ![Image d’action en ligne SharePoint 7](./media/connectors-create-api-sharepointonline/action-7.png)  
9. Sélectionnez hello **le contenu du fichier** contrôler et entrez contenu hello qui sera écrit toohello fichier qui sera créé. Pour le contenu du fichier hello, notez que vous pouvez utiliser une des propriétés hello de déclencheur hello que vous avez créé précédemment. Il suffit de sélectionner les propriétés hello dans liste hello présentée. Vous pouvez également entrer hello **le contenu du fichier** texte directement dans le contrôle de hello. Dans cet exemple, nous sélectionnons certaines propriétés et ajoutons des espaces et un tiret entre chaque propriété.        
   ![Image d’action en ligne SharePoint 8](./media/connectors-create-api-sharepointonline/action-8.png)  
10. Enregistrer le flux de travail hello modifications tooyour  
11. Félicitations, vous avez maintenant une application entièrement fonctionnelle logique qui est déclenchée lorsqu’un nouvel élément est ajouté de liste SharePoint Online de tooa. application Hello crée ensuite un fichier, à l’aide de certaines des propriétés hello à partir d’un élément de liste hello.  Vous pouvez maintenant le tester en créant un nouvel élément de liste SharePoint de hello. 

