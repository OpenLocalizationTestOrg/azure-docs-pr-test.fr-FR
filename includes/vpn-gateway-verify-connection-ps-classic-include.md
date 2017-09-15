<span data-ttu-id="4c096-101">Vous pouvez vérifier que votre connexion a réussi à l’aide de l’applet de commande « Get-AzureVNetConnection ».</span><span class="sxs-lookup"><span data-stu-id="4c096-101">You can verify that your connection succeeded by using the 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="4c096-102">Utilisez l’exemple d’applet de commande suivant, en configurant les valeurs sur les vôtres.</span><span class="sxs-lookup"><span data-stu-id="4c096-102">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="4c096-103">Le nom du réseau virtuel doit être placé entre guillemets s’il contient des espaces.</span><span class="sxs-lookup"><span data-stu-id="4c096-103">The name of the virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="4c096-104">Une fois l’applet de commande exécutée, affichez les valeurs.</span><span class="sxs-lookup"><span data-stu-id="4c096-104">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="4c096-105">Dans l’exemple ci-dessous, la zone État de la connectivité indique « Connecté » et vous pouvez voir les octets d’entrée et de sortie.</span><span class="sxs-lookup"><span data-stu-id="4c096-105">In the example below, the Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : The connectivity state for the local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal