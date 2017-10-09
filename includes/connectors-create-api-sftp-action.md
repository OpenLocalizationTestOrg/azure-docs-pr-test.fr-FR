Maintenant que vous avez ajouté un déclencheur, son heure de toodo quelque chose intéressante avec des données hello sont générées par le déclencheur de hello. Suivez ces étapes de tooadd un Bonjour **SFTP - dossier d’extraction** action. Cette action extrait contenu hello d’un fichier si les conditions hello définies sont remplies. 

tooconfigure hello cette action, vous devez hello tooprovide informations suivantes. Vous remarquerez qu’il s’agit de données simple toouse générées par le déclencheur de hello en tant qu’entrée pour certaines des propriétés hello pour le nouveau fichier de hello :

| SFTP - propriété Extraire un dossier | Description |
| --- | --- |
| Chemin d’accès du fichier d’archive source |Il s’agit de chemin d’accès de hello pour le fichier hello en cours d’extraction. Vous pouvez sélectionner un des jetons de hello à partir d’une action antérieure ou parcourir le chemin de fichier hello SFTP server toofind hello. |
| Chemin de destination du dossier |Il s’agit de chemin d’accès hello où seront placés les fichiers hello extraite. Vous pouvez sélectionner un des jetons de hello à partir d’une action antérieure en tant que chemin d’accès de destination hello ou parcourir le serveur SFTP de hello et sélectionnez un chemin d’accès. |
| Remplacer ? |Indique si un fichier avec hello même nom que celui que hello avez extrait le fichier se trouve dans le chemin d’accès de dossier de destination hello si le fichier existant de hello doit être remplacé ou non. |

Commençons Ajout hello action tooextract hello fichiers si condition hello définie précédemment a la valeur trop*True*. 

1. Sélectionnez **Ajouter une action**.        
   ![Image de condition d’action SFTP 6](./media/connectors-create-api-sftp/condition-6.png)   
2. Sélectionnez hello **SFTP - dossier d’extraction** action      
   ![Image de condition d’action SFTP 7](./media/connectors-create-api-sftp/condition-7.png)   
3. Sélectionnez **Chemin d’accès du fichier d’archive source**            .  
   ![Image de condition d’action SFTP 9](./media/connectors-create-api-sftp/condition-9.png)   
4. Sélectionnez hello **chemin d’accès du fichier** jeton. Cela indique que vous allez utiliser le chemin d’accès du fichier hello du fichier hello hello déclencheur trouvé en tant que chemin d’accès du fichier archive source hello.           
   ![Image de condition d’action SFTP 10](./media/connectors-create-api-sftp/condition-10.png)   
5. Sélectionnez **Chemin de destination du dossier**         .  
   ![Image de condition d’action SFTP 11](./media/connectors-create-api-sftp/condition-11.png)   
6. Sélectionnez hello **chemin d’accès du fichier** jeton. Cela indique que vous allez utiliser le chemin d’accès de fichier hello du fichier hello hello déclencheur trouvée en tant que chemin d’accès de destination hello pour les fichiers de hello extraite.   
7. Entrez *\ExtractedFile* Bonjour **chemin d’accès du dossier de Destination** contrôle. Cela juste après le jeton de chemin d’accès du fichier hello Bonjour contrôle de chemin d’accès de dossier de Destination.         
   ![Image de condition d’action SFTP 12](./media/connectors-create-api-sftp/condition-12.png)   
8. Entrez *True* Bonjour **remplacer ?* tooindicate de contrôle des fichiers existants doivent être remplacés s’ils ont hello comme hello du même nom extrait les fichiers.      
   ![Image de condition d’action SFTP 13](./media/connectors-create-api-sftp/condition-13.png)   
9. Enregistrer le flux de travail hello modifications tooyour  

