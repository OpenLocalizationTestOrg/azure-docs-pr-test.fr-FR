## <a name="using-vault-credentials-tooauthenticate-with-hello-azure-backup-service"></a>À l’aide de tooauthenticate des informations d’identification de coffre avec hello service Azure Backup
Hello locale server (client Windows ou un serveur Windows Server ou de Data Protection Manager) doit toobe authentifiée avec un coffre de sauvegarde avant qu’il peut sauvegarder des données tooAzure. l’authentification de Hello est obtenue à l’aide de « informations d’identification de coffre ». concept de Hello d’informations d’identification de coffre est un concept toohello similaire d’un fichier « paramètres de publication » qui est utilisé dans Azure PowerShell.

### <a name="what-is-hello-vault-credential-file"></a>Qu’est le fichier d’informations d’identification de coffre hello ?
fichier d’informations d’identification de coffre Hello est un certificat généré par le portail hello chaque coffre de sauvegarde. portail de Hello télécharge ensuite toohello de clé publique hello Access Control Service (ACS). clé privée de Hello du certificat de hello est effectuée utilisateur toohello disponibles dans le cadre du flux de travail hello qui est fournie sous la forme d’une entrée dans le workflow de l’inscription d’ordinateur hello. Cela permet d’authentifier hello machine toosend les données de sauvegarde tooan identifié coffre Bonjour service Azure Backup.

informations d’identification de coffre Hello sont utilisée uniquement pendant le flux de travail de l’inscription hello. Il est tooensure de responsabilité de l’utilisateur hello qui hello des informations d’identification de coffre fichier n’est pas compromis. S’il est compris entre les mains hello de n’importe quel utilisateur non autorisé, fichier d’informations d’identification de coffre hello peut être utilisé tooregister autres ordinateurs hello même coffre. Toutefois, comme les données de sauvegarde hello sont chiffrées à l’aide d’une phrase secrète qui appartient toohello client, les données de sauvegarde existantes ne peut pas être compromises. toomitigate ce problème, les informations d’identification de coffre sont définies tooexpire dans 48hrs. Vous pouvez télécharger des informations d’identification de coffre hello d’un coffre de sauvegarde n’importe quel nombre de fois, mais uniquement hello dernière coffre d’informations d’identification est applicable au cours de flux de travail de l’inscription hello.

### <a name="download-hello-vault-credential-file"></a>Télécharger le fichier d’informations d’identification de coffre hello
fichier d’informations d’identification de coffre Hello est téléchargé via un canal sécurisé à partir de hello portail Azure. Hello service Azure Backup n’a pas connaissance de la clé privée de hello du certificat de hello et la clé privée de hello n’est pas conservé dans le portail de hello ou un service de hello. Utilisez hello suivant les étapes toodownload hello coffre informations d’identification du fichier tooa ordinateur local.

1. Connectez-vous à toohello [portail de gestion](https://manage.windowsazure.com/)
2. Cliquez sur **Services de récupération** dans le volet de navigation gauche hello et coffre de sauvegarde hello select que vous avez créée. Cliquez sur hello cloud icône tooget toohello vue démarrage rapide hello du coffre de sauvegarde.
   
   ![Aperçu rapide](./media/backup-download-credentials/quickview.png)
3. Dans la page de démarrage rapide de hello, cliquez sur **informations d’identification du coffre de téléchargement**. portail de Hello génère fichier d’informations d’identification du coffre de hello qui devient disponible en téléchargement.
   
   ![Télécharger](./media/backup-download-credentials/downloadvc.png)
4. portail de Hello générera une information d’identification de coffre à l’aide d’une combinaison de nom de l’archivage hello et hello date actuelle. Cliquez sur **enregistrer** toodownload hello coffre informations d’identification toohello du compte local télécharge le dossier ou sélectionnez Enregistrer sous à partir de hello enregistrer menu toospecify un emplacement pour les informations d’identification de coffre hello.

### <a name="note"></a>Remarque
* Vérifiez que les informations d’identification de coffre hello est enregistré dans un emplacement qui est accessible à partir de votre ordinateur. S’il est stocké dans un partage de fichier/SMB, recherchez les autorisations d’accès hello.
* fichier d’informations d’identification de coffre Hello est utilisé uniquement pendant le flux de travail de l’inscription hello.
* fichier d’informations d’identification de coffre Hello expire au bout de 48hrs et peut être téléchargé à partir du portail de hello.
* Consultez toohello Azure Backup [FAQ](../articles/backup/backup-azure-backup-faq.md) pour toute question sur le flux de travail hello.

