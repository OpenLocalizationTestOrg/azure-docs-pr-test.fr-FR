#### <a name="toostop-and-start-a-virtual-device"></a>toostop et démarrer un appareil virtuel
toostop un appareil virtuel, cliquez sur son nom, puis cliquez sur **arrêt**. Pendant l’arrêt de l’appareil virtuel de hello, son état est **arrêt**. Une fois un appareil virtuel hello est arrêté, son état est **arrêté**.

Utilisez hello suivant toostop d’applets de commande et démarrez un appareil virtuel.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a>toorestart un appareil virtuel
Lorsqu’un périphérique virtuel est en cours d’exécution et que vous souhaitez toorestart, cliquez sur son nom, puis cliquez sur **redémarrer**. Pendant le redémarrage de périphérique virtuel de hello, son état est **redémarrage**. Quand un appareil virtuel hello est prêt à vous toouse, son état est **en cours d’exécution**.

Utilisez hello suivant l’applet de commande toorestart un appareil virtuel.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

