# <a name="common-errors-during-classic-tooazure-resource-manager-migration"></a>Erreurs courantes lors classique tooAzure migration du Gestionnaire de ressources
Catalogues de cet article hello des erreurs et des solutions d’atténuation plus courants lors de la migration de hello des ressources IaaS de pile de déploiement classique Azure modèle toohello Azure Resource Manager.

## <a name="list-of-errors"></a>Liste d’erreurs
| Chaîne d’erreur | Atténuation |
| --- | --- |
| Erreur interne du serveur |Dans certains cas, il s’agit d’une erreur temporaire qui disparaît à la tentative suivante. S’il continue toopersist, [contactez le support Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) besoins d’examen des journaux de la plateforme. <br><br> **Remarque :** une fois que l’incident de hello est suivi par l’équipe de support hello, n’essayez pas tout atténuation automatique car cela peut avoir des conséquences inattendues sur votre environnement. |
| La migration n’est pas prise en charge pour le déploiement {deployment-name} dans le service hébergé {hosted-service-name} car il s’agit d’un déploiement PaaS (Web/Worker). |Cela se produit lorsque le déploiement contient un rôle web/de travail. Étant donné que la migration est uniquement prise en charge pour les Machines virtuelles, veuillez supprimer hello/rôle de déploiement de hello et réessayez la migration. |
| Échec du déploiement du modèle {template-name}. CorrelationId={guid} |Dans hello back-end du service de migration, nous utilisons des ressources de toocreate modèles Azure Resource Manager dans la pile du Gestionnaire de ressources Azure hello. Étant donné que les modèles sont idempotents, généralement vous pouvez réessayer en toute sécurité tooget d’opération de migration hello au-delà de cette erreur. Si cette erreur persiste toopersist, veuillez [contactez le support Azure](../articles/azure-supportability/how-to-create-azure-support-request.md) et leur accorder hello CorrelationId. <br><br> **Remarque :** une fois que l’incident de hello est suivi par l’équipe de support hello, n’essayez pas tout atténuation automatique car cela peut avoir des conséquences inattendues sur votre environnement. |
| réseau virtuel de Hello {virtual-network-name} n’existe pas. |Cela peut se produire si vous avez créé hello réseau virtuel dans le nouveau portail de Azure hello. nom de réseau virtuel réel Hello suit le modèle de hello « groupe * <VNET name>» |
| La machine virtuelle {vm-name} du service hébergé {hosted-service-name} contient une extension {extension-name} qui n’est pas prise en charge dans Azure Resource Manager. Il est recommandé de toouninstall à partir de hello machine virtuelle avant de poursuivre la migration. |Les extensions XML telles que BGInfo 1.* ne sont pas prises en charge dans Azure Resource Manager. Par conséquent, elles ne peuvent pas faire l’objet d’une migration. Si ces extensions sont gauche hello installés sur virtual machine, ils sont automatiquement désinstallés avant la fin de la migration hello. |
| La machine virtuelle {vm-name} du service hébergé {hosted-service-name} contient l’extension VMSnapshot/VMSnapshotLinux, dont la migration n’est actuellement pas prise en charge. Désinstaller de hello machine virtuelle et l’ajouter à l’aide de Azure Resource Manager une fois hello Migration est terminée. |Il s’agit de scénario hello où hello virtual machine est configurée pour Azure Backup. Étant donné que ce scénario n’est actuellement pas pris en charge, procédez comme solution de contournement hello à https://aka.ms/vmbackupmigration |
| Machine virtuelle {vm-name} dans le service hébergé {hébergé-service-name} contient l’Extension {extension-name}, dont l’état n’est pas signalée à partir de la machine virtuelle de hello. Par conséquent, elle ne peut pas faire l’objet d’une migration. Vérifiez que hello état de l’Extension est signalé ou désinstaller l’extension de hello à partir de la machine virtuelle de hello et recommencez la migration. <br><br> La machine virtuelle {vm-name} du service hébergé {hosted-service-name} contient une extension {extension-name} qui génère l’état de gestionnaire : {handler-status}. Par conséquent, hello machine virtuelle ne peut pas être migré. Vérifiez que le statut de gestionnaire d’Extension hello signalé est {gestionnaire-status} ou désinstallez-la de hello machine virtuelle et recommencez la migration. <br><br> Agent de machine virtuelle pour la machine virtuelle {vm-name} dans le service hébergé {hébergé-service-name} est reporting hello état global de l’agent comme n’étant pas prêt. Par conséquent, hello machine virtuelle ne pas être migrée, s’il a une extension peut être migrée. Assurez-vous que l’Agent de machine virtuelle hello est signalent l’état de l’agent global comme prêt. Consultez toohttps://aka.ms/classiciaasmigrationfaqs. |L’agent invité Azure et les Extensions de machine virtuelle doivent sortant internet access toohello VM stockage compte toopopulate leur état. Causes les plus courantes d’échec de l’état : <li> un groupe de sécurité réseau qui bloque l’accès sortant toohello internet <li> Si hello réseau virtuel a local sur les serveurs DNS et connectivité DNS est perdu <br><br> Si vous continuez toosee un état non pris en charge, vous pouvez désinstaller hello extensions tooskip cette vérification et déplacer vers le bas dans la migration. |
| La migration n’est pas prise en charge pour le déploiement {deployment-name} dans le service hébergé {hosted-service-name} car il contient plusieurs groupes à haute disponibilité. |Actuellement, seuls les services hébergés contenant au maximum un groupe à haute disponibilité peuvent faire l’objet d’une migration. toowork résoudre ce problème, déplacez hello supplémentaire à haute disponibilité et de machines virtuelles dans ces tooa d’ensembles de disponibilité différent d’un service hébergé. |
| La migration n’est pas prise en charge pour le déploiement {déploiement-name} dans le service hébergé {hébergé-service-name, car il possède des machines virtuelles qui ne font pas partie de hello à haute disponibilité même si le service hébergé de hello contient un. |solution de contournement Hello pour ce scénario est tooeither déplacer tous les ordinateurs virtuels hello dans une disponibilité unique définir ou supprimer tous les ordinateurs virtuels à partir de hello à haute disponibilité dans le service hébergé de hello. |
| Compte/le service hébergé/virtuel de stockage réseau {virtual-network-name} est en cours de hello en cours de migration et il ne peut pas être changé |Cette erreur se produit lorsque hello opération de migration « Préparer » a été effectué sur la ressource de hello et une opération qui pourrait permettre une ressource de toohello de modification est déclenchée. En raison de verrou hello sur le plan de gestion hello après l’opération de « Préparation », n’importe quelle ressource de toohello de modifications sont bloquées. plan de gestion toounlock hello, vous pouvez exécuter hello « Valider » migration opération toocomplete la migration ou hello « Annuler » migration opération tooroll précédent hello opération de « Préparation ». |
| La migration n’est pas autorisée pour le service hébergé {hosted-service-name} car il contient une machine virtuelle {vm-name} à l’état : RoleStateUnknown. La migration est autorisée uniquement lorsque hello machine virtuelle est dans un des éléments suivants de hello États - en cours d’exécution, arrêté, arrêté désalloué. |Hello machine virtuelle peut être en cours via une transition d’état, ce qui se produit généralement lorsque lors d’une opération de mise à jour sur hello le service hébergé comme un redémarrage, etc. installation de l’extension. Il est recommandé pour toocomplete d’opération de mise à jour hello sur le service hébergé de hello avant la tentative de migration. |
| Déploiement {déploiement-name} dans le service hébergé {hébergé-service-name} contient une machine virtuelle {vm-name} avec un disque de données {données-disque-name} dont {size-of-the-vhd-blob-backing-the-data-disk} de la taille en octets blob physique ne correspond pas à {de taille logique hello disque de données de machine virtuelle Size-of-the-Data-Disk-specified-in-the-VM-API} octets. La migration va être effectuée sans spécification d’une taille de disque de données hello pour hello Azure Resource Manager VM. | Cette erreur se produit si vous avez redimensionné blob de disque dur virtuel hello sans mettre à jour de la taille de hello dans le modèle de machine virtuelle API hello. Vous trouverez les étapes de correction détaillées [ci-dessous](#vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-the-vm-data-disk-logical-size-bytes).|
| Une exception de stockage s’est produite lors de la validation du disque de données {nom du disque de données} avec le lien du support {URI du disque de données} pour la machine virtuelle {nom de la machine virtuelle} dans le service cloud {nom du service cloud}. Vérifiez que ce lien de support de disque dur virtuel hello est accessible à cet ordinateur virtuel | Cette erreur peut se produire si les disques hello Hello machine virtuelle a été supprimé ou n’est pas plus accessible. Assurez-vous que disques hello pour hello machine virtuelle existe.|
| La machine virtuelle {nom de la machine virtuelle} dans le service hébergé {nom du service cloud} contient un disque avec un élément MediaLink {vhd-uri} ayant le nom d’objet blob {vhd-nom d’objet blob} qui n’est pas pris en charge dans Azure Resource Manager. | Cette erreur se produit lorsque hello du nom d’objet blob de hello est « / » y n'est pas prise en charge dans le fournisseur de ressources de calcul actuellement. |
| La migration n’est pas autorisée pour le déploiement {déploiement-name} dans le service hébergé {cloud-service-name}, car il n’est pas dans la portée régionale de hello. Consultez toohttp://aka.ms/regionalscope pour déplacer cette étendue tooregional de déploiement. | En 2014, Azure a annoncé que les ressources réseau seront déplace d’une étendue de tooregional de niveau de la portée de cluster. Pour plus d’informations ( http://aka.ms/regionalscope ), consultez l’article [ http://aka.ms/regionalscope ]. Cette erreur se produit lorsque le déploiement hello en cours de migration n’a pas une opération de mise à jour, ce qui déplace automatiquement portée régionale de tooa. Meilleure solution est tooeither ajouter un point de terminaison de tooa machine virtuelle ou données disque toohello machine virtuelle et recommencez la migration. <br> Consultez [comment tooset des points de terminaison sur un ordinateur de virtuel Windows classique dans Azure](../articles/virtual-machines/windows/classic/setup-endpoints.md#create-an-endpoint) ou [attacher une machine virtuelle données disque tooa Windows créée avec le modèle de déploiement classique de hello](../articles/virtual-machines/windows/classic/attach-disk.md)|


## <a name="detailed-mitigations"></a>Étapes de correction détaillées

### <a name="vm-with-data-disk-whose-physical-blob-size-bytes-does-not-match-hello-vm-data-disk-logical-size-bytes"></a>Machine virtuelle avec disque de données taille en octets d’objets blob dont physique ne correspond pas à octets de taille logique de disque de données de machine virtuelle hello.

Cela se produit lorsque hello taille logique de disque de données peut obtenir synchronisée avec la taille du blob hello réelle disque dur virtuel. Cela peut être facilement vérifié à l’aide de hello suivant de commandes :

#### <a name="verifying-hello-issue"></a>Vérification de problème de hello

```PowerShell
# Store hello VM details in hello VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

# Display hello data disk properties
# NOTE hello data disk LogicalDiskSizeInGB below which is 11GB. Also note hello MediaLink Uri of hello VHD blob as we'll use this in hello next step
$vm.VM.DataVirtualHardDisks


HostCaching         : None
DiskLabel           : 
DiskName            : coreosvm-coreosvm-0-201611230636240687
Lun                 : 0
LogicalDiskSizeInGB : 11
MediaLink           : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
SourceMediaLink     : 
IOType              : Standard
ExtensionData       : 

# Now get hello properties of hello blob backing hello data disk above
# NOTE hello size of hello blob is about 15 GB which is different from LogicalDiskSizeInGB above
$blob = Get-AzureStorageblob -Blob "coreosvm-dd1.vhd" -Container vhds 

$blob

ICloudBlob        : Microsoft.WindowsAzure.Storage.Blob.CloudPageBlob
BlobType          : PageBlob
Length            : 16106127872
ContentType       : application/octet-stream
LastModified      : 11/23/2016 7:16:22 AM +00:00
SnapshotTime      : 
ContinuationToken : 
Context           : Microsoft.WindowsAzure.Commands.Common.Storage.AzureStorageContext
Name              : coreosvm-dd1.vhd
```

#### <a name="mitigating-hello-issue"></a>Atténuation de problème de hello

```PowerShell
# Convert hello blob size in bytes tooGB into a variable which we'll use later
$newSize = [int]($blob.Length / 1GB)

# See hello calculated size in GB
$newSize

15

# Store hello disk name of hello data disk as we'll use this tooidentify hello disk toobe updated
$diskName = $vm.VM.DataVirtualHardDisks[0].DiskName

# Identify hello LUN of hello data disk tooremove
$lunToRemove = $vm.VM.DataVirtualHardDisks[0].Lun

# Now remove hello data disk from hello VM so that hello disk isn't leased by hello VM and it's size can be updated
Remove-AzureDataDisk -LUN $lunToRemove -VM $vm | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       213xx1-b44b-1v6n-23gg-591f2a13cd16   Succeeded  

# Verify we have hello right disk that's going toobe updated
Get-AzureDisk -DiskName $diskName

AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : 
Location             : East US
DiskSizeInGB         : 11
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 0c56a2b7-a325-123b-7043-74c27d5a61fd
OperationStatus      : Succeeded

# Now update hello disk toohello new size
Update-AzureDisk -DiskName $diskName -ResizedSizeInGB $newSize -Label $diskName

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureDisk     cv134b65-1b6n-8908-abuo-ce9e395ac3e7 Succeeded 

# Now verify that hello "DiskSizeInGB" property of hello disk matches hello size of hello blob 
Get-AzureDisk -DiskName $diskName


AffinityGroup        : 
AttachedTo           : 
IsCorrupted          : False
Label                : coreosvm-coreosvm-0-201611230636240687
Location             : East US
DiskSizeInGB         : 15
MediaLink            : https://contosostorage.blob.core.windows.net/vhds/coreosvm-dd1.vhd
DiskName             : coreosvm-coreosvm-0-201611230636240687
SourceImageName      : 
OS                   : 
IOType               : Standard
OperationDescription : Get-AzureDisk
OperationId          : 1v53bde5-cv56-5621-9078-16b9c8a0bad2
OperationStatus      : Succeeded

# Now we'll add hello disk back toohello VM as a data disk. First we need tooget an updated VM object
$vm = Get-AzureVM -ServiceName $servicename -Name $vmname

Add-AzureDataDisk -Import -DiskName $diskName -LUN 0 -VM $vm -HostCaching ReadWrite | Update-AzureVm -Name $vmname -ServiceName $servicename

OperationDescription OperationId                          OperationStatus
-------------------- -----------                          ---------------
Update-AzureVM       b0ad3d4c-4v68-45vb-xxc1-134fd010d0f8 Succeeded      
```

### <a name="moving-a-vm-tooa-different-subscription-after-completing-migration"></a>Déplacement d’un machine virtuelle tooa autre abonnement après avoir effectué la migration

Après avoir terminé le processus de migration hello, vous souhaiterez abonnement de tooanother toomove hello machine virtuelle. Toutefois, si vous avez un code secret ou du certificat sur hello déplacer des ordinateurs virtuels qui fait référence à une ressource du coffre de clés, hello est actuellement pas pris en charge. Hello ci-dessous les instructions vous permettra de problème de hello tooworkaround. 

#### <a name="powershell"></a>PowerShell
```powershell
$vm = Get-AzureRmVM -ResourceGroupName "MyRG" -Name "MyVM"
Remove-AzureRmVMSecret -VM $vm
Update-AzureRmVM -ResourceGroupName "MyRG" -VM $vm
```
#### <a name="azure-cli-20"></a>Azure CLI 2.0

```bash
az vm update -g "myrg" -n "myvm" --set osProfile.Secrets=[]
```
