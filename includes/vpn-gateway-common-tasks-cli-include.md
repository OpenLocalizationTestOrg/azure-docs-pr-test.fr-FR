### <a name="tooview-local-network-gateways"></a>passerelles de réseau local tooview

tooview une liste des passerelles de réseau local hello, utilisez hello [liste de local-passerelle de réseau az](https://docs.microsoft.com/cli/azure/network/local-gateway#list) commande.

```azurecli
az network local-gateway list --resource-group TestRG1
```

[!INCLUDE [modify-prefix](vpn-gateway-modify-ip-prefix-cli-include.md)]

[!INCLUDE [modify-gateway-IP](vpn-gateway-modify-lng-gateway-ip-cli-include.md)]

### <a name="tooverify-hello-shared-key-values"></a>valeurs de clé tooverify hello partagé

Vérifiez que valeur de clé hello partagé est hello la même valeur que vous avez utilisé pour la configuration de votre périphérique VPN. Si elle n’est pas le cas, exécutez connexion hello à nouveau à l’aide de la valeur hello à partir de l’appareil de hello ou mettre à jour d’appareil de hello valeur hello hello retour. les valeurs Hello doivent correspondre. tooview hello partagé clé, utilisez hello [liste de connexions vpn de réseau az](https://docs.microsoft.com/cli/azure/network/vpn-connection#list).

```azurecli
az network vpn-connection shared-key show --connection-name VNet1toSite2 --resource-group TestRG1
```
### <a name="tooview-hello-vpn-gateway-public-ip-address"></a>passerelle VPN de hello tooview adresse IP publique

toofind hello adresse IP publique de votre passerelle de réseau virtuel, utilisez hello [liste public-ip de réseau az](https://docs.microsoft.com/cli/azure/network/public-ip#list) commande. Pour faciliter la lecture, sortie hello pour cet exemple est liste de hello toodisplay mis en forme des adresses IP publiques au format de table.

```azurecli
az network public-ip list --resource-group TestRG1 --output table
```
