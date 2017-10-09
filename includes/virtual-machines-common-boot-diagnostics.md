La prise en charge de deux fonctionnalités de débogage est désormais disponible dans Azure : les supports de Console Output et Screenshot pour le modèle de déploiement Azure Virtual Machines Resource Manager. 

Lors de la prochaine tooAzure de votre propre image ou même initialisation d’une des images de plateforme hello, il peut y avoir plusieurs raisons pour lesquelles un ordinateur virtuel Obtient dans un état non démarrable. Activation de ces fonctionnalités vous tooeasily diagnostiquer et récupérer vos Machines virtuelles des échecs de démarrage.

Pour les Machines virtuelles Linux, vous pouvez facilement afficher sortie hello de votre journal de console à partir de hello portail :

![Portail Azure](./media/virtual-machines-common-boot-diagnostics/screenshot1.png)
 
Toutefois, pour Windows et les ordinateurs virtuels Linux, Azure permet également de toosee une capture d’écran de hello machine virtuelle à partir de l’hyperviseur de hello :

![Error](./media/virtual-machines-common-boot-diagnostics/screenshot2.png)

Ces deux fonctionnalités sont prises en charge par les Machines Virtuelles Azure dans toutes les régions. Tooappear de minutes too10 dans votre compte de stockage peuvent prendre note des captures d’écran et la sortie.

## <a name="common-boot-errors"></a>Erreurs de démarrage courantes

- [0xC000000E](https://support.microsoft.com/help/4010129)
- [0xC000000F](https://support.microsoft.com/help/4010130)
- [0xC0000011](https://support.microsoft.com/help/4010134)
- [0xC0000034](https://support.microsoft.com/help/4010140)
- [0xC0000098](https://support.microsoft.com/help/4010137)
- [0xC00000BA](https://support.microsoft.com/help/4010136)
- [0xC000014C](https://support.microsoft.com/help/4010141)
- [0xC0000221](https://support.microsoft.com/help/4010132)
- [0xC0000225](https://support.microsoft.com/help/4010138)
- [0xC0000359](https://support.microsoft.com/help/4010135)
- [0xC0000605](https://support.microsoft.com/help/4010131)
- [Système d’exploitation introuvable.](https://support.microsoft.com/help/4010142)
- [Échec de démarrage ou INACCESSIBLE_BOOT_DEVICE.](https://support.microsoft.com/help/4010143)

## <a name="enable-diagnostics-on-a-new-virtual-machine"></a>Activer la fonction de diagnostic sur une nouvelle machine virtuelle
1. Lorsque vous créez une Machine virtuelle à partir de la version préliminaire du portail de hello, sélectionnez hello **Azure Resource Manager** à partir de la liste déroulante modèle de déploiement hello :
 
    ![Gestionnaire de ressources](./media/virtual-machines-common-boot-diagnostics/screenshot3.jpg)

2. Configurer hello analyse option tooselect hello de stockage Azure où vous aimeriez tooplace ces fichiers de diagnostic.
 
    ![Créer une machine virtuelle](./media/virtual-machines-common-boot-diagnostics/screenshot4.jpg)

3. Si vous déployez un modèle Azure Resource Manager, accédez de ressource d’ordinateur virtuel tooyour et ajouter la section de profil de diagnostics hello. N’oubliez pas d’en-tête de version de l’API de toouse hello « 2015-06-15 ».

    ```json
    {
          "apiVersion": "2015-06-15",
          "type": "Microsoft.Compute/virtualMachines",
          … 
    ```

4. profil de diagnostic Hello vous permet de compte de stockage hello tooselect où vous souhaitez tooput ces journaux.

    ```json
            "diagnosticsProfile": {
                "bootDiagnostics": {
                "enabled": true,
                "storageUri": "[concat('http://', parameters('newStorageAccountName'), '.blob.core.windows.net')]"
                }
            }
            }
        }
    ```

toodeploy un exemple de Machine virtuelle avec les diagnostics de démarrage activées, consultez notre référentiel ici.

## <a name="update-an-existing-virtual-machine"></a>Mettre à jour une machine virtuelle existante ##

diagnostics de démarrage tooenable via hello Portal, vous pouvez également mettre à jour un ordinateur virtuel existant via hello portail. Sélectionnez hello option Diagnostics de démarrage et les enregistrer. Redémarrez l’effet de tootake hello machine virtuelle.

![Mettre à jour une machine virtuelle existante](./media/virtual-machines-common-boot-diagnostics/screenshot5.png)

