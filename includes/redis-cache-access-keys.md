instance de Cache Redis Azure tooconnect tooan, les clients de cache doivent nom d’hôte hello, les ports et les clés de cache de hello. Certains clients peuvent faire référence à des éléments toothese par des noms légèrement différents. Vous pouvez récupérer ces informations dans hello portail Azure ou à l’aide des outils de ligne de commande tels que CLI d’Azure.

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a>Récupérer le nom d’hôte, les ports et les clés d’accès à l’aide de hello portail Azure
tooretrieve nom d’hôte, ports et les clés d’accès à l’aide de hello portail Azure, [Parcourir](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) cache tooyour Bonjour [portail Azure](https://portal.azure.com) et cliquez sur **clés d’accès** et  **Propriétés** Bonjour **menu ressource**. 

![Paramètres du cache Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a>Récupération du nom d’hôte, des ports et des clés d’accès à l’aide de l’interface de ligne de commande Azure
nom d’hôte tooretrieve hello et les ports à l’aide d’Azure CLI 2.0, vous pouvez appeler [afficher de redis az](https://docs.microsoft.com/cli/azure/redis#show)et les clés de hello tooretrieve que vous pouvez appeler [az redis liste des clés](https://docs.microsoft.com/cli/azure/redis#list-keys). Hello script suivant appelle ces deux commandes et devez hello nom d’hôte, les ports et console toohello de clés.

```azurecli
#/bin/bash

# Retrieve hello hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve hello hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve hello keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display hello retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

Pour plus d’informations sur ce script, consultez [obtenir le nom d’hôte hello, les ports et les clés Azure Redis cache](../articles/redis-cache/scripts/cache-keys-ports.md). Pour plus d’informations sur Azure CLI 2.0, consultez [Installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) et [Prise en main d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).
