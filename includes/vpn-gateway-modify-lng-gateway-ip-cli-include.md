### <a name="toomodify-hello-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="8dead-101">passerelle de réseau local toomodify hello 'gatewayIpAddress'</span><span class="sxs-lookup"><span data-stu-id="8dead-101">toomodify hello local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="8dead-102">Si le périphérique VPN de hello que vous souhaitez tooconnect toohas modifié son adresse IP publique, vous devez tooreflect de passerelle du réseau local d’hello toomodify qui changent.</span><span class="sxs-lookup"><span data-stu-id="8dead-102">If hello VPN device that you want tooconnect toohas changed its public IP address, you need toomodify hello local network gateway tooreflect that change.</span></span> <span data-ttu-id="8dead-103">adresse IP de passerelle Hello peut être modifié sans supprimer une connexion de passerelle VPN existante (si vous avez un).</span><span class="sxs-lookup"><span data-stu-id="8dead-103">hello gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="8dead-104">d’adresses IP de passerelle toomodify hello, remplacer des valeurs hello 'Site2' et 'TestRG1' par votre propre à l’aide de hello [mise à jour de local-passerelle de réseau az](https://docs.microsoft.com/cli/azure/network/local-gateway#update) commande.</span><span class="sxs-lookup"><span data-stu-id="8dead-104">toomodify hello gateway IP address, replace hello values 'Site2' and 'TestRG1' with your own using hello [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="8dead-105">Vérifiez que l’adresse IP de hello est correct dans la sortie de hello :</span><span class="sxs-lookup"><span data-stu-id="8dead-105">Verify that hello IP address is correct in hello output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```