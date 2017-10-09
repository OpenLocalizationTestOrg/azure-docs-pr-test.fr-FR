Vous pouvez vous connecter tooa machine virtuelle qui est déployé tooyour réseau virtuel en créant une machine virtuelle de tooyour connexion Bureau à distance. Hello meilleure manière tooinitially vérifier que vous pouvez vous connecter à tooyour machine virtuelle est tooconnect par à l’aide de son IP privé d’adresses, au lieu du nom de l’ordinateur. De cette façon, vous testez toosee si vous pouvez vous connecter, pas si la résolution de noms est configurée correctement.

1. Recherchez l’adresse IP privée de hello. Vous trouverez les adresse IP privée hello d’une machine virtuelle de plusieurs façons. Ci-dessous, nous affichons les étapes hello pour hello portail Azure et PowerShell.

  - Portail Azure - recherchez votre machine virtuelle Bonjour portail Azure. Afficher les propriétés de hello de hello machine virtuelle. adresse IP privée de Hello est répertorié.

  - PowerShell - utilisation hello exemple tooview une liste des ordinateurs virtuels et des adresses IP privées à partir de vos groupes de ressources. Vous n’avez pas besoin toomodify cet exemple avant de l’utiliser.

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

2. Vérifiez que vous êtes connecté tooyour réseau virtuel à l’aide de la connexion VPN de hello.
3. Ouvrez **connexion Bureau à distance** en tapant « RDP » ou « Connexion Bureau à distance » dans la zone de recherche de hello sur la barre des tâches hello, puis sélectionnez Connexion Bureau à distance. Vous pouvez également ouvrir la connexion Bureau à distance à l’aide de la commande « mstsc » hello dans PowerShell. 
4. Connexion Bureau à distance, entrez les adresse IP privée hello Hello machine virtuelle. Vous pouvez cliquez sur « Afficher les Options » tooadjust les paramètres supplémentaires, puis vous connecter.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot un tooa de connexion RDP machine virtuelle

Si vous rencontrez des problèmes de connexion d’ordinateur virtuel de tooa sur votre connexion VPN, vérifiez suivantes de hello :

- Vérifiez que votre connexion VPN aboutit.
- Vérifiez que vous vous connectez toohello une adresse IP privée pour hello machine virtuelle.
- Si vous pouvez vous connecter toohello machine virtuelle à l’aide d’IP privé de hello adresse, mais ne Hello pas de nom de l’ordinateur, vérifiez que vous avez correctement configuré DNS. Pour plus d’informations sur le fonctionnement de la résolution de noms pour les machines virtuelles, consultez [Résolution de noms pour les machines virtuelles](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
- Pour plus d’informations sur les connexions RDP, consultez [tooa de connexions de résoudre les problèmes de bureau à distance VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
