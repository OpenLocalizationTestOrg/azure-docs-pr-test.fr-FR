Avec Azure Resource Manager, vous définissez des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé. modèle de Hello inclut une section appelée paramètres qui contient toutes les valeurs de paramètre hello.
Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou dans l’environnement hello que vous effectuez le déploiement. Ne définissez pas de paramètres pour les valeurs qui resteront toujours hello même. Chaque valeur de paramètre est utilisé dans hello de toodefine modèle hello déploiement des ressources. 

Lorsque vous définissez des paramètres, utilisez hello **allowedValues** toospecify champ dont les valeurs d’un utilisateur peut fournir au cours du déploiement. Hello d’utilisation **defaultValue** champ tooassign un paramètre de toohello value, si aucune valeur n’est fournie au cours du déploiement.

Nous allons examiner chaque paramètre dans le modèle de hello.

### <a name="logicappname"></a>logicAppName
nom de Hello de hello logique application toocreate.

    "logicAppName": {
        "type": "string"
    }