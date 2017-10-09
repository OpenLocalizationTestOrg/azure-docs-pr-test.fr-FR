Lorsque vous n’avez plus besoin un disque de données est attachée tooa virtual machine, vous pouvez facilement la détacher. Détachement d’un disque supprime le disque de hello à partir de l’ordinateur virtuel de hello, mais ne supprime pas les disques hello de hello compte de stockage Azure.

Si vous souhaitez toouse hello données existantes hello disque à nouveau, vous pouvez rattacher il toohello même ordinateur virtuel ou un autre.  

> [!NOTE]
> toodetach un disque de système d’exploitation, vous devez tout d’abord toodelete hello virtual machine.
>

## <a name="find-hello-disk"></a>Trouver de disque de hello
Si vous ne connaissez nom hello de hello disque ou souhaitez tooverify avant de vous détacher, procédez comme suit.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).

2. Cliquez sur **virtuels**, et puis sélectionnez hello machine virtuelle appropriée.

3. Cliquez sur **disques** le long de hello bord gauche du tableau de bord de machine virtuelle hello, sous **paramètres**.

 tableau de bord de machine virtuelle Hello répertorie le nom de hello et type de tous les disques attachés. Par exemple, cet écran affiche une machine virtuelle avec un disque de système d’exploitation et un disque de données :

    ![Rechercher un disque de données](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a>Détacher un disque de hello
1. À partir de hello portail Azure, cliquez sur **virtuels**, puis cliquez sur nom hello de machine virtuelle hello qui possède le disque de données hello souhaité toodetach.

2. Cliquez sur **disques** le long de hello bord gauche du tableau de bord de machine virtuelle hello, sous **paramètres**.

3. Cliquez sur le disque hello toodetach.

  ![Identifier hello disque toodetach](./media/howto-detach-disk-windows-linux/disklist.png)

4. Dans la barre de commandes hello, cliquez sur **détachement**.

  ![Recherchez hello detach, commande](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. Dans la fenêtre de confirmation hello, cliquez sur **Oui** disque de hello toodetach.

  ![Confirmer le détachement du disque hello](./media/howto-detach-disk-windows-linux/confirmdetach.png)

disque de Hello reste dans le stockage, mais n’est plus attaché tooa virtual machine.
