#### <a name="toostop-and-start-a-cloud-appliance"></a>toostop et démarrer une application cloud

1. toostop un dispositif de cloud, accédez toohello machine virtuelle pour votre solution de cloud.
    ![Machine virtuelle StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart1.png)

2. Dans la barre de commandes hello, cliquez sur **arrêter**.

    ![Machine virtuelle StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart2.png)

3. Cliquez sur **Oui**lorsque vous êtes invité à confirmer l’opération.

    ![Machine virtuelle StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart3.png)

4. Lorsque vous arrêtez une machine virtuelle, celle-ci est désallouée. Pendant l’arrêt de l’équipement de cloud hello, son état est **Deallocating**. Une fois que le matériel de cloud hello est arrêté, son état est **arrêté (désallouée)**.

    ![Machine virtuelle StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart4.png)

5. Une fois qu’une machine virtuelle est arrêtée, cliquez sur **Démarrer** (bouton devient disponible) toostart hello machine virtuelle. Une fois que le matériel de cloud hello a démarré, son état est **démarré**.

    ![Machine virtuelle StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart5.png)

Utilisez hello suivant toostop d’applets de commande et démarrer une application cloud.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-cloud-appliance"></a>toorestart un dispositif de cloud

toorestart un dispositif de cloud, accédez toohello machine virtuelle pour votre solution de cloud. Dans la barre de commandes hello, cliquez sur **redémarrer**. Lorsque vous y êtes invité, confirmez hello redémarrage. Lorsque le dispositif de cloud hello est prêt à vous toouse, son état est **en cours d’exécution**.

![Machine virtuelle StorSimple Cloud Appliance](./media/storsimple-8000-stop-restart-cloud-appliance/sca-stop-restart6.png)

Utilisez hello suivant l’applet de commande toorestart un dispositif de cloud.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

