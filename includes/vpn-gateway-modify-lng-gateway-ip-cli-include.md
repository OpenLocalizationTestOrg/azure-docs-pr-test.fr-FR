### <a name="to-modify-the-local-network-gateway-gatewayipaddress"></a><span data-ttu-id="6431a-101">Pour modifier la passerelle de réseau local « gatewayIpAddress »</span><span class="sxs-lookup"><span data-stu-id="6431a-101">To modify the local network gateway 'gatewayIpAddress'</span></span>

<span data-ttu-id="6431a-102">Si le périphérique VPN auquel vous souhaitez vous connecter a changé son adresse IP publique, vous devez modifier la passerelle de réseau local pour refléter cette modification.</span><span class="sxs-lookup"><span data-stu-id="6431a-102">If the VPN device that you want to connect to has changed its public IP address, you need to modify the local network gateway to reflect that change.</span></span> <span data-ttu-id="6431a-103">L’adresse IP de passerelle peut être modifiée sans supprimer de connexion de passerelle VPN existante (si vous en possédez une).</span><span class="sxs-lookup"><span data-stu-id="6431a-103">The gateway IP address can be changed without removing an existing VPN gateway connection (if you have one).</span></span> <span data-ttu-id="6431a-104">Pour modifier l’adresse IP de passerelle, remplacez les valeurs « Site2 » et « TestRG1 » par vos propres valeurs à l’aide de la commande [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update).</span><span class="sxs-lookup"><span data-stu-id="6431a-104">To modify the gateway IP address, replace the values 'Site2' and 'TestRG1' with your own using the [az network local-gateway update](https://docs.microsoft.com/cli/azure/network/local-gateway#update) command.</span></span>

```azurecli
az network local-gateway update --gateway-ip-address 23.99.222.170 --name Site2 --resource-group TestRG1
```

<span data-ttu-id="6431a-105">Vérifiez que l’adresse IP est correcte dans la sortie :</span><span class="sxs-lookup"><span data-stu-id="6431a-105">Verify that the IP address is correct in the output:</span></span>

```
"gatewayIpAddress": "23.99.222.170",
```