<span data-ttu-id="452c2-101">Vous pouvez vérifier que votre connexion a réussi à l’aide d’applet de commande hello 'Get-AzureRmVirtualNetworkGatewayConnection', avec ou sans '-déboguer ».</span><span class="sxs-lookup"><span data-stu-id="452c2-101">You can verify that your connection succeeded by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="452c2-102">Hello utilisez exemple d’applet de commande suivant, la configuration de hello valeurs toomatch votre propre.</span><span class="sxs-lookup"><span data-stu-id="452c2-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="452c2-103">Si vous y êtes invité, sélectionnez « A » dans l’ordre toorun 'All'.</span><span class="sxs-lookup"><span data-stu-id="452c2-103">If prompted, select 'A' in order toorun 'All'.</span></span> <span data-ttu-id="452c2-104">Dans l’exemple de hello, '-nom » fait référence nom toohello de connexion hello que vous souhaitez tootest.</span><span class="sxs-lookup"><span data-stu-id="452c2-104">In hello example, '-Name' refers toohello name of hello connection that you want tootest.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="452c2-105">Une fois que l’applet de commande hello terminée, afficher les valeurs de hello.</span><span class="sxs-lookup"><span data-stu-id="452c2-105">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="452c2-106">Dans l’exemple hello ci-dessous, état de la connexion hello montre comme « Connecté » et que vous pouvez le voir octets d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="452c2-106">In hello example below, hello connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```