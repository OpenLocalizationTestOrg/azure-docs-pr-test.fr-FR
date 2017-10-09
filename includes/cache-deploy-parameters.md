
### <a name="cacheskuname"></a>cacheSKUName
niveau de tarification Hello Hello nouveau Azure Redis Cache.

    "cacheSKUName": {
      "type": "string",
      "allowedValues": [
        "Basic",
        "Standard"
      ],
      "defaultValue": "Basic",
      "metadata": {
        "description": "hello pricing tier of hello new Azure Redis Cache."
      }
    },

modèle de Hello définit les valeurs hello sont autorisées pour ce paramètre (base ou Standard) et affecte la valeur par défaut (Basic) si aucune valeur n’est spécifiée. Basic fournit un nœud unique avec plusieurs tailles disponibles too53 go.
Norme fournit deux nœuds principal/réplica avec plusieurs tailles disponibles too53 Go et 99,9 % de contrat SLA.

### <a name="cacheskufamily"></a>cacheSKUFamily
famille de Hello pour hello référence (SKU).

    "cacheSKUFamily": {
      "type": "string",
      "allowedValues": [
        "C"
      ],
      "defaultValue": "C",
      "metadata": {
        "description": "hello family for hello sku."
      }
    },


### <a name="cacheskucapacity"></a>cacheSKUCapacity
taille de Hello de la nouvelle instance de Cache Redis Azure hello. 

    "cacheSKUCapacity": {
      "type": "int",
      "allowedValues": [
        0,
        1,
        2,
        3,
        4,
        5,
        6
      ],
      "defaultValue": 0,
      "metadata": {
        "description": "hello size of hello new Azure Redis Cache instance. "
      }
    }


modèle de Hello définit les valeurs hello qui sont autorisées pour ce paramètre (0, 1, 2, 3, 4, 5 ou 6) et affecte la valeur par défaut (1) si aucune valeur n’est spécifiée. Ces chiffres correspondent à des tailles de cache toofollowing : 0 = 250 Mo, 1 = 1 Go, 2 = 2,5 Go, 3 = 6 Go, 4 = 13 Go, 5 = 26 Go, 6 = 53 Go

