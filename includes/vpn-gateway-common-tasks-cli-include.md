### <a name="tooview-local-network-gateways"></a><span data-ttu-id="a2bfd-101">passerelles de réseau local tooview</span><span class="sxs-lookup"><span data-stu-id="a2bfd-101">tooview local network gateways</span></span>

<span data-ttu-id="a2bfd-102">tooview une liste des passerelles de réseau local hello, utilisez hello [liste de local-passerelle de réseau az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) commande.</span><span class="sxs-lookup"><span data-stu-id="a2bfd-102">tooview a list of hello local network gateways, use hello [az network local-gateway list](https://docs.microsoft.com/cli/azure/network/local-gateway#list) command.</span></span>

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a><span data-ttu-id="a2bfd-103">valeurs de clé tooverify hello partagé</span><span class="sxs-lookup"><span data-stu-id="a2bfd-103">tooverify hello shared key values</span></span>

<span data-ttu-id="a2bfd-104">Vérifiez que valeur de clé hello partagé est hello la même valeur que vous avez utilisé pour la configuration de votre périphérique VPN.</span><span class="sxs-lookup"><span data-stu-id="a2bfd-104">Verify that hello shared key value is hello same value that you used for your VPN device configuration.</span></span> <span data-ttu-id="a2bfd-105">Si elle n’est pas le cas, exécutez connexion hello à nouveau à l’aide de la valeur hello à partir de l’appareil de hello ou mettre à jour d’appareil de hello valeur hello hello retour.</span><span class="sxs-lookup"><span data-stu-id="a2bfd-105">If it is not, either run hello connection again using hello value from hello device, or update hello device with hello value from hello return.</span></span> <span data-ttu-id="a2bfd-106">les valeurs Hello doivent correspondre.</span><span class="sxs-lookup"><span data-stu-id="a2bfd-106">hello values must match.</span></span> <span data-ttu-id="a2bfd-107">tooview hello partagé clé, utilisez hello [liste de connexions vpn de réseau az](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span><span class="sxs-lookup"><span data-stu-id="a2bfd-107">tooview hello shared key, use hello [az network vpn-connection-list](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).</span></span>

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a><span data-ttu-id="a2bfd-108">passerelle VPN de hello tooview adresse IP publique</span><span class="sxs-lookup"><span data-stu-id="a2bfd-108">tooview hello VPN gateway Public IP address</span></span>

<span data-ttu-id="a2bfd-109">toofind hello adresse IP publique de votre passerelle de réseau virtuel, utilisez hello [liste public-ip de réseau az](https://docs.microsoft.com/cli/azure/network/public-ip#list) commande.</span><span class="sxs-lookup"><span data-stu-id="a2bfd-109">toofind hello public IP address of your virtual network gateway, use hello [az network public-ip list](https://docs.microsoft.com/cli/azure/network/public-ip#list) command.</span></span> <span data-ttu-id="a2bfd-110">Pour faciliter la lecture, sortie hello pour cet exemple est liste de hello toodisplay mis en forme des adresses IP publiques au format de table.</span><span class="sxs-lookup"><span data-stu-id="a2bfd-110">For easy reading, hello output for this example is formatted toodisplay hello list of public IPs in table format.</span></span>

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
