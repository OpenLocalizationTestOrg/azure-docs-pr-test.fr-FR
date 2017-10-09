
Pour plus d’informations sur les disques, consultez l’article [À propos des disques et VHD pour machines virtuelles](../articles/virtual-machines/linux/about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

<a id="attachempty"></a>

## <a name="attach-an-empty-disk"></a>Attacher un disque vide
1. Ouvrez Azure CLI 1.0 et [connecter tooyour abonnement Azure](../articles/xplat-cli-connect.md). Assurez-vous que vous êtes en mode Azure Service Management (`azure config mode asm`).
2. Entrez `azure vm disk attach-new` toocreate et connectez un nouveau disque, comme indiqué dans hello l’exemple suivant. Remplacez *myVM* avec le nom hello de votre Machine virtuelle de Linux et spécifiez la taille hello du disque de hello en Go, ce qui est *100 Go* dans cet exemple :

    ```azurecli
    azure vm disk attach-new myVM 100
    ```

3. Une fois le disque de données hello est créé et attaché, il est répertorié dans la sortie de hello de `azure vm disk list <virtual-machine-name>` comme indiqué dans hello l’exemple suivant :
   
    ```azurecli
    azure vm disk list TestVM
    ```

    Hello la sortie est similaire toohello l’exemple suivant :

    ```bash
    info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        myVM-2645b8030676c8f8.vhd  Linux
     data:    0    100       myVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

<a id="attachexisting"></a>

## <a name="attach-an-existing-disk"></a>Association d'un disque existant
Pour attacher un disque existant, vous devez disposer d’un fichier .vhd dans un compte de stockage.

1. Ouvrez Azure CLI 1.0 et [connecter tooyour abonnement Azure](../articles/xplat-cli-connect.md). Assurez-vous que vous êtes en mode Azure Service Management (`azure config mode asm`).
2. Vérifier si hello disque dur virtuel que vous souhaitez tooattach est déjà téléchargée tooyour abonnement Azure :
   
    ```azurecli
    azure vm disk list
    ```

    Hello la sortie est similaire toohello l’exemple suivant :

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
     data:    Name                                          OS
     data:    --------------------------------------------  -----
     data:    myTestVhd                                     Linux
     data:    TestVM-ubuntuVMasm-0-201508060029150744  Linux
     data:    TestVM-ubuntuVMasm-0-201508060040530369
     info:    vm disk list command OK
    ```

3. Si vous ne trouvez pas les disques hello que vous souhaitez toouse, vous risquez de télécharger un abonnement tooyour de disque dur virtuel local à l’aide de `azure vm disk create` ou `azure vm disk upload`. Un exemple de `disk create` serait comme hello l’exemple suivant :
   
    ```azurecli
    azure vm disk create myVhd .\TempDisk\test.VHD -l "East US" -o Linux
    ```

    Hello la sortie est similaire toohello l’exemple suivant :

    ```azurecli
    info:    Executing command vm disk create
    + Retrieving storage accounts
    info:    VHD size : 10 GB
    info:    Uploading 10485760.5 KB
    Requested:100.0% Completed:100.0% Running:   0 Time:   25s Speed:    82 KB/s
    info:    Finishing computing MD5 hash, 16% is complete.
    info:    https://mystorageaccount.blob.core.windows.net/disks/myVHD.vhd was
    uploaded successfully
    info:    vm disk create command OK
    ```
   
   Vous pouvez également utiliser `azure vm disk upload` tooupload un compte de stockage de disque dur virtuel tooa. Lire plus hello commandes toomanage vos disques de données de machine virtuelle Azure [ici](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

4. Maintenant vous attachez hello souhaitée virtuels tooyour de disque dur virtuel :
   
    ```azurecli
    azure vm disk attach myVM myVhd
    ```
   
   Assurez-vous que tooreplace *myVM* avec nom hello de votre machine virtuelle, et *myVHD* avec votre disque dur virtuel souhaité.

5. Vous pouvez vérifier le disque de hello est attaché toohello machine virtuelle `azure vm disk list <virtual-machine-name>`:
   
    ```azurecli
    azure vm disk list myVM
    ```

    Hello la sortie est similaire toohello l’exemple suivant :

    ```azurecli
     info:    Executing command vm disk list
   
   * Fetching disk images
   * Getting virtual machines
   * Getting VM disks
     data:    Lun  Size(GB)  Blob-Name                         OS
     data:    ---  --------  --------------------------------  -----
     data:         30        TestVM-2645b8030676c8f8.vhd  Linux
     data:    1    10        test.VHD
     data:    0    100        TestVM-76f7ee1ef0f6dddc.vhd
     info:    vm disk list command OK
    ```

> [!NOTE]
> Après avoir ajouté un disque de données, vous devez toolog sur l’ordinateur virtuel de toohello et initialiser le disque de hello donc hello virtual machine peut utiliser un disque de hello pour le stockage (voir hello suivant les étapes pour plus d’informations sur comment toodo initialiser le disque de hello).
> 
> 

