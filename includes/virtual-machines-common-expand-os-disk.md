## <a name="overview"></a>Vue d'ensemble
Lorsque vous créez un nouvel ordinateur virtuel (VM) dans un groupe de ressources en déployant une image à partir de [Azure Marketplace](https://azure.microsoft.com/marketplace/), lecteur de système d’exploitation hello par défaut est de 127 Go. Même si elle est toohello de disques de données tooadd possible VM (selon le nombre hello référence (SKU) que vous avez choisie) et plus il est recommandé tooinstall applications et charges de travail intensives du processeur sur ces disques addenda, les clients doivent souvent tooexpand hello du système d’exploitation lecteur toosupport certains scénarios tels que les éléments suivants :

1. Prendre en charge les applications héritées qui installent des composants sur le lecteur du système d’exploitation.
2. Migrer un ordinateur physique ou une machine virtuelle depuis un emplacement local avec un lecteur de système d’exploitation plus volumineux.

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : Resource Manager et classique. Cet article décrit à l’aide du modèle de gestionnaire de ressources hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.
> 
> 

## <a name="resize-hello-os-drive"></a>Redimensionner le lecteur de hello du système d’exploitation
Dans cet article nous allons faire hello de redimensionnement lecteur hello du système d’exploitation à l’aide des modules de gestionnaire de ressources de [Azure Powershell](/powershell/azureps-cmdlets-docs). Ouvrez votre fenêtre Powershell ou Powershell ISE en mode administrateur et suivez les étapes de hello ci-dessous :

1. Connectez-vous tooyour Microsoft Azure dans le mode de gestion des ressources de compte et sélectionnez votre abonnement comme suit :
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. Définissez le nom du groupe de ressources et le nom de la machine virtuelle comme suit :
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. Obtenir une référence de tooyour machine virtuelle comme suit :
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. Arrêter hello machine virtuelle avant de redimensionner le disque de hello comme suit :
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. Et ici proviennent moment hello que nous avons attend ! Définir la taille de valeur de hello du système d’exploitation disque toohello souhaité hello et mettre à jour de hello machine virtuelle comme suit :
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > Hello nouvelle taille doit être supérieure à la taille du disque existant hello. Hello maximale autorisée est de 1 023 go.
   > 
   > 
6. Mise à jour hello machine virtuelle peut prendre quelques secondes. Une fois la commande hello fin d’exécution, redémarrez hello machine virtuelle comme suit :
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

Vous avez terminé. Maintenant RDP dans hello machine virtuelle, ouvrez Gestion de l’ordinateur (ou de gestion des disques) et développez le lecteur hello hello qui vient d’être l’espace alloué à l’aide de.

## <a name="summary"></a>Résumé
Dans cet article, nous avons utilisé les modules Powershell tooexpand Hello lecteur du système d’exploitation d’une machine virtuelle IaaS Azure Resource Manager. Reproduite ci-dessous est complète du script hello de référence :

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a>Étapes suivantes
Bien que dans cet article, nous principalement sur l’expansion de disque hello du système d’exploitation de machine virtuelle de hello, hello développé script peut également être utilisé pour le développement hello données disques attachés toohello machine virtuelle en modifiant une seule ligne de code. Par exemple, tooexpand hello commencez par les données de disque attaché toohello machine virtuelle, remplacez hello ```OSDisk``` objet de ```StorageProfile``` avec ```DataDisks``` de tableau et utilisez un tooobtain index numérique un disque de données attaché toofirst de référence, comme indiqué ci-dessous :

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
De même vous pouvez référencer d’autres disques de données attaché toohello machine virtuelle, à l’aide d’un index comme indiqué ci-dessus ou hello ```Name``` propriété du disque hello comme illustré ci-dessous :

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

Si vous souhaitez toofind out comment tooattach disques tooan Azure Resource Manager VM, activez cette option [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

