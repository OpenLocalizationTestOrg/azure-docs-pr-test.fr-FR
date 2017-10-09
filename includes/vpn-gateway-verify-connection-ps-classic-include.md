<span data-ttu-id="7dc3b-101">Vous pouvez vérifier que votre connexion a réussi à l’aide d’applet de commande hello 'Get-AzureVNetConnection'.</span><span class="sxs-lookup"><span data-stu-id="7dc3b-101">You can verify that your connection succeeded by using hello 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="7dc3b-102">Hello utilisez exemple d’applet de commande suivant, la configuration de hello valeurs toomatch votre propre.</span><span class="sxs-lookup"><span data-stu-id="7dc3b-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="7dc3b-103">nom de Hello du réseau virtuel de hello doit être entre guillemets si elle contient des espaces.</span><span class="sxs-lookup"><span data-stu-id="7dc3b-103">hello name of hello virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="7dc3b-104">Une fois que l’applet de commande hello terminée, afficher les valeurs de hello.</span><span class="sxs-lookup"><span data-stu-id="7dc3b-104">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="7dc3b-105">Dans l’exemple hello ci-dessous, état de la connectivité hello indique « Connecté », et vous pouvez voir des octets d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="7dc3b-105">In hello example below, hello Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal