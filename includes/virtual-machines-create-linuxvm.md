
1. Se connecter tooyour abonnement Azure à l’aide des étapes hello répertoriées dans [connecter tooAzure de hello Azure CLI 1.0](../articles/xplat-cli-connect.md).

2. Assurez-vous que vous êtes en mode de déploiement classique hello comme suit :

    ```azurecli
    azure config mode asm
    ```

3. Découvrez image de hello Linux que vous souhaitez tooload à partir d’images disponibles de hello comme suit :

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    Dans une fenêtre d’invite de commandes Windows, utilisez **find** au lieu de grep.
   
4. Utilisez `azure vm create` toocreate une machine virtuelle avec l’image de Linux hello à partir de la liste précédente hello. Cette étape crée un service cloud et un compte de stockage. Vous pourriez également vous connecter cet machine virtuelle tooan service cloud existant avec un `-c` option. Créer un toolog de point de terminaison SSH dans la machine virtuelle Linux de toohello hello `-e` option. Hello exemple suivant crée un ordinateur virtuel nommé `myVM` à l’aide de hello `Ubuntu-14_04_4-LTS` image Bonjour `West US` emplacement et ajoute un nom d’utilisateur `ops`:
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    Hello la sortie est similaire toohello l’exemple suivant :

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > Pour une machine virtuelle Linux, vous devez fournir hello `-e` option `vm create`. Il n’est pas possible de tooenable SSH après la création de la machine virtuelle de hello. Pour plus d’informations sur SSH, lisez [comment tooUse SSH avec Linux sur Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

5. Vous pouvez vérifier les attributs hello Hello machine virtuelle à l’aide de hello `azure vm show` commande. Hello exemple suivant répertorie les informations pour hello ordinateur virtuel nommé `myVM`:

    ```azurecli   
    azure vm show myVM
    ```

6. Démarrez votre machine virtuelle avec hello `azure vm start` commande comme suit :

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur toutes les commandes de ces machines virtuelles Azure CLI 1.0, consultez hello [Using hello Azure CLI 1.0 avec l’API du déploiement classique hello](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

