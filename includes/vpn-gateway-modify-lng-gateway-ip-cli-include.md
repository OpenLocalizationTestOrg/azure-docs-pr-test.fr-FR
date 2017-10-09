### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a>passerelle de réseau local toomodify hello 'gatewayIpAddress'

Si le périphérique VPN de hello que vous souhaitez tooconnect toohas modifié son adresse IP publique, vous devez tooreflect de passerelle du réseau local d’hello toomodify qui changent. adresse IP de passerelle Hello peut être modifié sans supprimer une connexion de passerelle VPN existante (si vous avez un). d’adresses IP de passerelle toomodify hello, remplacer des valeurs hello 'Site2' et 'TestRG1' par votre propre à l’aide de hello [mise à jour de local-passerelle de réseau az](https://docs.microsoft.com/cli/azure/network/local-gateway#update) commande.

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

Vérifiez que l’adresse IP de hello est correct dans la sortie de hello :

```
"gatewayIpAddress": "23.99.222.170",
```