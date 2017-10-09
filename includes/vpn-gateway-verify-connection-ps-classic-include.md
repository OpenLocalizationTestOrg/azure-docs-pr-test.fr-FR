Vous pouvez vérifier que votre connexion a réussi à l’aide d’applet de commande hello 'Get-AzureVNetConnection'.

1. Hello utilisez exemple d’applet de commande suivant, la configuration de hello valeurs toomatch votre propre. nom de Hello du réseau virtuel de hello doit être entre guillemets si elle contient des espaces.

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. Une fois que l’applet de commande hello terminée, afficher les valeurs de hello. Dans l’exemple hello ci-dessous, état de la connectivité hello indique « Connecté », et vous pouvez voir des octets d’entrée et de sortie.

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal