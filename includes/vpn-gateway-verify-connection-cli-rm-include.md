Vous pouvez vérifier que votre connexion a réussi à l’aide de hello [az réseau-connexion vpn afficher](/cli/azure/network/vpn-connection#show) commande. Dans l’exemple de hello, '--nom » fait référence nom toohello de connexion hello que vous souhaitez tootest. Lors de la connexion de hello est en cours de hello d’établie, son état de connexion indique « Connexion ». Une fois que hello est établie, hello l’état too'Connected'.

```azurecli
az network vpn-connection show --name VNet1toSite2 --resource-group TestRG1
```

