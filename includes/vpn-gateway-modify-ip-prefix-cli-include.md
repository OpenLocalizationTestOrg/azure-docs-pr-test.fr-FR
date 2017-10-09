### <a name="noconnection"></a>préfixes d’adresses toomodify réseau local passerelle IP - aucune connexion de passerelle

Si vous n’avez pas une connexion de passerelle et vous souhaitez tooadd ou supprimez des préfixes d’adresses IP, vous utilisez hello même commande que vous utilisez passerelle de réseau local toocreate hello, [az réseau local-passerelle créer](https://docs.microsoft.com/cli/azure/network/local-gateway#create). Vous pouvez également utiliser cette adresse IP de passerelle commande tooupdate hello pour le périphérique VPN de hello. paramètres actuels de toooverwrite hello, utilisez nom existant de hello de votre passerelle de réseau local. Si vous utilisez un autre nom, vous créez une nouvelle passerelle de réseau local, au lieu de remplacer hello existant.

Chaque fois que vous apportez une modification, une hello intégralité de la liste de préfixes doit être spécifié, pas seulement hello préfixes que vous souhaitez toochange. Spécifier les préfixes hello uniquement que vous souhaitez tookeep. Dans ce cas, 10.0.0.0/24 et 20.0.0.0/24

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --connection-name TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

### <a name="withconnection"></a>toomodify réseau local passerelle préfixes d’adresses IP - connexion de passerelle existante

Si vous disposez d’une connexion de passerelle et souhaitez tooadd ou supprimez des préfixes d’adresses IP, vous pouvez mettre à jour à l’aide de préfixes d’espaces de hello [mise à jour de la passerelle locale az réseau](https://docs.microsoft.com/cli/azure/network/local-gateway#update). Cela entraînera une interruption de votre connexion VPN. Lors de la modification d’adresse IP de hello préfixes, vous n’avez pas besoin passerelle VPN de hello toodelete.

Chaque fois que vous apportez une modification, une hello intégralité de la liste de préfixes doit être spécifié, pas seulement hello préfixes que vous souhaitez toochange. Dans cet exemple, 10.0.0.0/24 et 20.0.0.0/24 sont déjà présents. Nous ajoutons hello préfixes 30.0.0.0/24 et 40.0.0.0/24 et que vous spécifiez tous les 4 des préfixes de hello lors de la mise à jour.

```azurecli
az network local-gateway update --local-address-prefixes 10.0.0.0/24 20.0.0.0/24 30.0.0.0/24 40.0.0.0/24 --name VNet1toSite2 --connection-name TestRG1
```