Vous pouvez vous connecter à une machine virtuelle déployée sur votre réseau virtuel en créant une connexion Bureau à distance à votre machine virtuelle. La meilleure méthode pour vérifier initialement que vous pouvez vous connecter à votre machine virtuelle consiste à vous connecter à l’aide de son adresse IP privée, plutôt qu’avec le nom d’ordinateur. Vous testez ainsi si vous pouvez vous connecter, que la résolution de nom soit configurée correctement ou non.

1. Recherchez l’adresse IP privée. L’adresse IP privée d’une machine virtuelle peut être trouvée en étudiant les propriétés de la machine virtuelle dans le portail Azure ou à l’aide de PowerShell.

  - Portail Azure : recherchez votre machine virtuelle dans le portail Azure. Affichez les propriétés de la machine virtuelle. L’adresse IP privée est répertoriée.

  - PowerShell : utilisez l’exemple pour afficher la liste des machines virtuelles et adresses IP privées de vos groupes de ressources. Vous n’avez pas besoin de modifier cet exemple pour pouvoir l’utiliser.

    ```powershell
    $VMs = Get-AzureRmVM
    $Nics = Get-AzureRmNetworkInterface | Where VirtualMachine -ne $null

    foreach($Nic in $Nics)
    {
      $VM = $VMs | Where-Object -Property Id -eq $Nic.VirtualMachine.Id
      $Prv = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAddress
      $Alloc = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAllocationMethod
      Write-Output "$($VM.Name): $Prv,$Alloc"
    }
    ```

2. Vérifiez que vous êtes connecté à votre réseau virtuel à l’aide de la connexion VPN point à site.
3. Ouvrez une **connexion Bureau à distance** en saisissant « RDP » ou « Connexion Bureau à distance » dans la zone de recherche de la barre des tâches, puis sélectionnez la connexion Bureau à distance. Vous pouvez également ouvrir une connexion Bureau à distance à l’aide de la commande « mstsc » dans PowerShell. 
4. Dans Connexion Bureau à distance, entrez l’adresse IP privée de la machine virtuelle. Vous pouvez cliquer sur « Afficher les Options » pour définir des paramètres supplémentaires, puis connectez-vous.

### <a name="to-troubleshoot-an-rdp-connection-to-a-vm"></a>Pour résoudre une connexion RDP à une machine virtuelle

Si vous rencontrez des problèmes de connexion à une machine virtuelle sur votre connexion VPN, vérifiez les points suivants :

- Vérifiez que votre connexion VPN aboutit.
- Vérifiez que vous vous connectez à l’adresse IP privée de la machine virtuelle.
- Utilisez « ipconfig » pour vérifier l’adresse IPv4 attribuée à l’adaptateur Ethernet sur l’ordinateur à partir duquel vous vous connectez. Si l’adresse IP est comprise dans la plage d’adresses du réseau virtuel auquel vous vous connectez, ou dans la plage d’adresses de votre VPNClientAddressPool, cette situation est désignée sous le terme d’espaces d’adressage qui se chevauchent. Lorsque vos espaces d’adressage se chevauchent de cette façon, le trafic réseau n’atteint pas Azure et reste sur le réseau local.
- Si vous pouvez vous connecter à la machine virtuelle à l’aide de l’adresse IP privée, mais pas à l’aide du nom d’ordinateur, vérifiez que vous avez correctement configuré DNS. Pour plus d’informations sur le fonctionnement de la résolution de noms pour les machines virtuelles, consultez [Résolution de noms pour les machines virtuelles](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
- Vérifiez que le package de configuration du client VPN a été généré après que les adresses IP du serveur DNS ont été spécifiées pour le réseau virtuel. Si vous avez mis à jour les adresses IP du serveur DNS, générez et installez un package de configuration du client VPN.
- Pour plus d’informations sur les connexions RDP, consultez [Résoudre des problèmes de connexion Bureau à distance à une machine virtuelle](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).