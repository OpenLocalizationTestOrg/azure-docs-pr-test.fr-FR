Avec Azure Resource Manager, vous définissez des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé. modèle de Hello inclut une section appelée paramètres qui contient toutes les valeurs de paramètre hello.
Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou dans l’environnement hello que vous effectuez le déploiement. Ne définissez pas de paramètres pour les valeurs qui resteront toujours hello même. Chaque valeur de paramètre est utilisé dans hello modèle toodefine hello ressources qui sont déployés. 

Lorsque vous définissez des paramètres, utilisez hello **allowedValues** toospecify champ dont les valeurs d’un utilisateur peut fournir au cours du déploiement. Hello d’utilisation **defaultValue** champ tooassign un paramètre de toohello value, si aucune valeur n’est fournie au cours du déploiement.

Nous allons examiner chaque paramètre dans le modèle de hello.

### <a name="sitename"></a>siteName
nom de Hello de hello l’application web que vous souhaitez toocreate.

    "siteName":{
      "type":"string"
    }

### <a name="hostingplanname"></a>hostingPlanName
nom Hello Hello du Service d’applications plan toouse pour l’hébergement de l’application web hello.

    "hostingPlanName":{
      "type":"string"
    }

### <a name="sku"></a>sku
Hello niveau tarifaire pour hello plan d’hébergement.

    "sku": {
      "type": "string",
      "allowedValues": [
        "F1",
        "D1",
        "B1",
        "B2",
        "B3",
        "S1",
        "S2",
        "S3",
        "P1",
        "P2",
        "P3",
        "P4"
      ],
      "defaultValue": "S1",
      "metadata": {
        "description": "hello pricing tier for hello hosting plan."
      }
    }

modèle de Hello définit les valeurs hello qui sont autorisées pour ce paramètre et affecte la valeur par défaut (S1) si aucune valeur n’est spécifiée.

### <a name="workersize"></a>workerSize
taille des instances Hello Hello (petite, moyen ou grand) de plan d’hébergement.

    "workerSize":{
      "type":"string",
      "allowedValues":[
        "0",
        "1",
        "2"
      ],
      "defaultValue":"0"
    }

modèle de Hello définit les valeurs hello qui sont autorisées pour ce paramètre (0, 1 ou 2) et affecte la valeur par défaut (0) si aucune valeur n’est spécifiée. les valeurs Hello correspondent toosmall, moyenne et grande.

