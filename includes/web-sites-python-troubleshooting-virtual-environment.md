script de déploiement Hello ignorera la création d’un environnement virtuel de hello sur Azure s’il détecte qu’il existe déjà un environnement virtuel compatible.  Ceci peut accélérer considérablement le déploiement.  Les packages déjà installés sont ignorés par pip.

Dans certaines situations, vous souhaiterez tooforce supprimer cet environnement virtuel.  Vous souhaiterez toodo cela si vous décidez de tooinclude un environnement virtuel en tant que partie de votre référentiel.  Vous pouvez également toodo cela si vous avez besoin de tooget rid de certains packages ou toorequirements.txt des modifications de test.

Il existe quelques hello de toomanage options existant d’un environnement virtuel sur Azure :

### <a name="option-1-use-ftp"></a>Option 1 : Utiliser FTP
Avec un client FTP, connecter toohello serveur et vous pourrez le dossier d’env toodelete en mesure de hello.  Notez que certains clients FTP (par exemple, les navigateurs web) peuvent être en lecture seule et ne permettent pas les dossiers toodelete, et il vous faudra toomake, toouse qu’un client FTP avec cette fonctionnalité.  nom d’hôte Hello FTP et d’utilisateur sont affichés dans le panneau de votre application web sur hello [Azure Portal](https://portal.azure.com).

### <a name="option-2-toggle-runtime"></a>Option 2 : Activer/désactiver runtime
Voici une alternative qui tire parti des faits hello que script de déploiement hello va supprimer le dossier d’env hello lorsqu’il n’est pas version souhaitée de hello de Python.  Cela sera efficacement supprimer l’environnement existant de hello et créer un nouveau.

1. Commutateur tooa autre version de Python (via runtime.txt ou hello **paramètres de l’Application** panneau Bonjour portail Azure)
2. git force certaines modifications (ignorez les erreurs d’installation pip, le cas échéant).
3. Version tooinitial arrière du commutateur de Python
4. git force à nouveau des modifications.

### <a name="option-3-customize-deployment-script"></a>Option 3 : Personnaliser le script de déploiement
Si vous avez personnalisé le script de déploiement hello, vous pouvez modifier hello code dans deploy.cmd tooforce de dossier d’env toodelete hello.

