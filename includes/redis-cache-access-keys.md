<span data-ttu-id="e9dbd-101">instance de Cache Redis Azure tooconnect tooan, les clients de cache doivent nom d’hôte hello, les ports et les clés de cache de hello.</span><span class="sxs-lookup"><span data-stu-id="e9dbd-101">tooconnect tooan Azure Redis Cache instance, cache clients need hello host name, ports, and keys of hello cache.</span></span> <span data-ttu-id="e9dbd-102">Certains clients peuvent faire référence à des éléments toothese par des noms légèrement différents.</span><span class="sxs-lookup"><span data-stu-id="e9dbd-102">Some clients may refer toothese items by slightly different names.</span></span> <span data-ttu-id="e9dbd-103">Vous pouvez récupérer ces informations dans hello portail Azure ou à l’aide des outils de ligne de commande tels que CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="e9dbd-103">You can retrieve this information in hello Azure portal or by using command-line tools such as Azure CLI.</span></span>

### <a name="retrieve-host-name-ports-and-access-keys-using-hello-azure-portal"></a><span data-ttu-id="e9dbd-104">Récupérer le nom d’hôte, les ports et les clés d’accès à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e9dbd-104">Retrieve host name, ports, and access keys using hello Azure Portal</span></span>
<span data-ttu-id="e9dbd-105">tooretrieve nom d’hôte, ports et les clés d’accès à l’aide de hello portail Azure, [Parcourir](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) cache tooyour Bonjour [portail Azure](https://portal.azure.com) et cliquez sur **clés d’accès** et  **Propriétés** Bonjour **menu ressource**.</span><span class="sxs-lookup"><span data-stu-id="e9dbd-105">tooretrieve host name, ports, and access keys using hello Azure Portal, [browse](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) tooyour cache in hello [Azure portal](https://portal.azure.com) and click **Access keys** and **Properties** in hello **Resource menu**.</span></span> 

![Paramètres du cache Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="e9dbd-107">Récupération du nom d’hôte, des ports et des clés d’accès à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="e9dbd-107">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="e9dbd-108">nom d’hôte tooretrieve hello et les ports à l’aide d’Azure CLI 2.0, vous pouvez appeler [afficher de redis az](https://docs.microsoft.com/cli/azure/redis#show)et les clés de hello tooretrieve que vous pouvez appeler [az redis liste des clés](https://docs.microsoft.com/cli/azure/redis#list-keys).</span><span class="sxs-lookup"><span data-stu-id="e9dbd-108">tooretrieve hello host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#show), and tooretrieve hello keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span></span> <span data-ttu-id="e9dbd-109">Hello script suivant appelle ces deux commandes et devez hello nom d’hôte, les ports et console toohello de clés.</span><span class="sxs-lookup"><span data-stu-id="e9dbd-109">hello following script calls these two commands and echos hello hostname, ports, and keys toohello console.</span></span>

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

<span data-ttu-id="e9dbd-110">Pour plus d’informations sur ce script, consultez [obtenir le nom d’hôte hello, les ports et les clés Azure Redis cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span><span class="sxs-lookup"><span data-stu-id="e9dbd-110">For more information about this script, see [Get hello hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="e9dbd-111">Pour plus d’informations sur Azure CLI 2.0, consultez [Installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) et [Prise en main d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e9dbd-111">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
