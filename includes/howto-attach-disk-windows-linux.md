


## <a name="attach-an-empty-disk"></a>Attacher un disque vide
Attachement d’un disque vide est un tooadd facilement des données sur le disque, car Azure crée un fichier .vhd de hello pour vous et la stocke dans le compte de stockage hello.

1. Cliquez sur **Machines virtuelles (classiques)**, et puis sélectionnez hello machine virtuelle appropriée.

2. Dans le menu Paramètres de hello, cliquez sur **disques**.

   ![Attacher un nouveau disque vide](./media/howto-attach-disk-windows-linux/menudisksattachnew.png)

3. Dans la barre de commandes hello, cliquez sur **attacher nouvelle**.  
    Hello **attacher un nouveau disque** boîte de dialogue s’affiche.

    ![Attacher un nouveau disque](./media/howto-attach-disk-windows-linux/newdiskdetail.png)

    Renseignez hello informations suivantes :
    - Dans **nom de fichier**, acceptez le nom par défaut de hello ou tapez-en un autre fichier .vhd de hello. disque de données Hello utilise un nom généré automatiquement, même si vous tapez un autre nom pour le fichier .vhd de hello.
    - Sélectionnez hello **Type** hello disque de données. Toutes les machines virtuelles prennent en charge des disques standard. La plupart prennent également en charge les disques Premium.
    - Sélectionnez hello **taille (Go)** hello disque de données.
    - Dans le champ **Mise en cache de l’hôte**, sélectionnez Aucune ou En lecture seule.
    - Cliquez sur OK toofinish.

4. Une fois le disque de données hello est créé et attaché, il est répertorié dans la section disques hello hello machine virtuelle.

   ![Nouveau disque de données vide correctement attaché](./media/howto-attach-disk-windows-linux/newdiskemptysuccessful.png)

> [!NOTE]
> Après avoir ajouté un disque de données, vous devez toolog sur toohello VM et initialisez le disque de hello afin qu’il peut être utilisé.

## <a name="how-to-attach-an-existing-disk"></a>Association d'un disque existant
Pour attacher un disque existant, vous devez disposer d’un fichier .vhd dans un compte de stockage. Hello d’utilisation [Add-AzureVhd](https://msdn.microsoft.com/library/azure/dn495173.aspx) compte de stockage toohello de fichier .vhd d’applet de commande tooupload hello. Une fois que vous avez créé et téléchargé le fichier .vhd de hello, vous pouvez les attacher à tooa machine virtuelle.

1. Cliquez sur **Machines virtuelles (classiques)**, et puis sélectionnez hello machine virtuelle appropriée.

2. Dans le menu Paramètres de hello, cliquez sur **disques**.

3. Dans la barre de commandes hello, cliquez sur **attacher existant**.

    ![Attacher un disque de données](./media/howto-attach-disk-windows-linux/menudisksattachexisting.png)

4. Cliquez sur **Emplacement**. affichent les comptes de stockage disponibles Hello. Sélectionnez ensuite un compte de stockage approprié dans la liste.

    ![Fournir un compte de stockage de disques](./media/howto-attach-disk-windows-linux/existdiskstorageaccounts.png)

5. Un **compte de stockage** dispose d’un ou plusieurs conteneurs qui contiennent des lecteurs de disque (VHD). Sélectionnez le conteneur approprié de hello depuis la rédaction.

    ![Fournir le conteneur de machines virtuelles windows](./media/howto-attach-disk-windows-linux/existdiskcontainers.png)

6. Hello **disques durs virtuels** panneau répertorie les lecteurs de disque hello contenues dans le conteneur de hello. Cliquez sur un des disques de hello, puis cliquez sur Sélectionner.

    ![Fournir une image de disque pour les machines virtuelles windows](./media/howto-attach-disk-windows-linux/existdiskvhds.png)

7. Hello **attachement du disque existant** panneau affiche à nouveau, à l’emplacement de hello contenant le compte de stockage hello conteneur et la machine virtuelle de disque dur sélectionné (vhd) tooadd toohello.

  Définissez **héberger la mise en cache** toonone ou en lecture seule, puis cliquez sur OK.

    ![Disque de données correctement attaché](./media/howto-attach-disk-windows-linux/exisitingdisksuccessful.png)
