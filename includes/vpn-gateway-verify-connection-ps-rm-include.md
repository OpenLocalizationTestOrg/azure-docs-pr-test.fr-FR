Vous pouvez vérifier que votre connexion a réussi à l’aide d’applet de commande hello 'Get-AzureRmVirtualNetworkGatewayConnection', avec ou sans '-déboguer ». 

1. Hello utilisez exemple d’applet de commande suivant, la configuration de hello valeurs toomatch votre propre. Si vous y êtes invité, sélectionnez « A » dans l’ordre toorun 'All'. Dans l’exemple de hello, '-nom » fait référence nom toohello de connexion hello que vous souhaitez tootest.

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. Une fois que l’applet de commande hello terminée, afficher les valeurs de hello. Dans l’exemple hello ci-dessous, état de la connexion hello montre comme « Connecté » et que vous pouvez le voir octets d’entrée et de sortie.
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```