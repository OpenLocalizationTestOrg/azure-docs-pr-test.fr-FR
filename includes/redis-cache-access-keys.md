<span data-ttu-id="b0733-101">Pour vous connecter à une instance Cache Redis Azure, vos clients de cache ont besoin du nom d’hôte, des ports et des clés du cache.</span><span class="sxs-lookup"><span data-stu-id="b0733-101">To connect to an Azure Redis Cache instance, cache clients need the host name, ports, and keys of the cache.</span></span> <span data-ttu-id="b0733-102">Certains clients peuvent référencer ces éléments par des noms légèrement différents.</span><span class="sxs-lookup"><span data-stu-id="b0733-102">Some clients may refer to these items by slightly different names.</span></span> <span data-ttu-id="b0733-103">Vous pouvez récupérer ces informations dans le portail Azure ou à l’aide des outils de ligne de commande tels qu’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b0733-103">You can retrieve this information in the Azure portal or by using command-line tools such as Azure CLI.</span></span>

### <a name="retrieve-host-name-ports-and-access-keys-using-the-azure-portal"></a><span data-ttu-id="b0733-104">Récupération du nom d’hôte, des ports et des clés d’accès à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="b0733-104">Retrieve host name, ports, and access keys using the Azure Portal</span></span>
<span data-ttu-id="b0733-105">Pour récupérer le nom d’hôte, les ports et les clés d’accès à l’aide du portail Azure, [accédez](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) à votre cache dans le [portail Azure](https://portal.azure.com) et cliquez sur **Clés d’accès** et **Propriétés** dans le **menu Ressource**.</span><span class="sxs-lookup"><span data-stu-id="b0733-105">To retrieve host name, ports, and access keys using the Azure Portal, [browse](../articles/redis-cache/cache-configure.md#configure-redis-cache-settings) to your cache in the [Azure portal](https://portal.azure.com) and click **Access keys** and **Properties** in the **Resource menu**.</span></span> 

![Paramètres du cache Redis](media/redis-cache-access-keys/redis-cache-hostname-ports-keys.png)

### <a name="retrieve-host-name-ports-and-access-keys-using-azure-cli"></a><span data-ttu-id="b0733-107">Récupération du nom d’hôte, des ports et des clés d’accès à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="b0733-107">Retrieve host name, ports, and access keys using Azure CLI</span></span>
<span data-ttu-id="b0733-108">Pour récupérer le nom d’hôte et les ports à l’aide d’Azure CLI 2.0, vous pouvez appeler [az redis show](https://docs.microsoft.com/cli/azure/redis#show), et pour récupérer les clés, vous pouvez appeler [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span><span class="sxs-lookup"><span data-stu-id="b0733-108">To retrieve the host name and ports using Azure CLI 2.0 you can call [az redis show](https://docs.microsoft.com/cli/azure/redis#show), and to retrieve the keys you can call [az redis list-keys](https://docs.microsoft.com/cli/azure/redis#list-keys).</span></span> <span data-ttu-id="b0733-109">Le script suivant appelle ces deux commandes et renvoie le nom d’hôte, les ports et les clés à la console.</span><span class="sxs-lookup"><span data-stu-id="b0733-109">The following script calls these two commands and echos the hostname, ports, and keys to the console.</span></span>

```azurecli
#/bin/bash

# Retrieve the hostname, ports, and keys for contosoCache located in contosoGroup

# Retrieve the hostname and ports for an Azure Redis Cache instance
redis=($(az redis show --name contosoCache --resource-group contosoGroup --query [hostName,enableNonSslPort,port,sslPort] --output tsv))

# Retrieve the keys for an Azure Redis Cache instance
keys=($(az redis list-keys --name contosoCache --resource-group contosoGroup --query [primaryKey,secondaryKey] --output tsv))

# Display the retrieved hostname, keys, and ports
echo "Hostname:" ${redis[0]}
echo "Non SSL Port:" ${redis[2]}
echo "Non SSL Port Enabled:" ${redis[1]}
echo "SSL Port:" ${redis[3]}
echo "Primary Key:" ${keys[0]}
echo "Secondary Key:" ${keys[1]}
```

<span data-ttu-id="b0733-110">Pour plus d’informations sur ce script, consultez [Obtenir le nom d’hôte, les ports et les clés pour Cache Redis Azure](../articles/redis-cache/scripts/cache-keys-ports.md).</span><span class="sxs-lookup"><span data-stu-id="b0733-110">For more information about this script, see [Get the hostname, ports, and keys for Azure Redis Cache](../articles/redis-cache/scripts/cache-keys-ports.md).</span></span> <span data-ttu-id="b0733-111">Pour plus d’informations sur Azure CLI 2.0, consultez [Installer Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) et [Prise en main d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b0733-111">For more information on Azure CLI 2.0, see [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) and [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli).</span></span>
