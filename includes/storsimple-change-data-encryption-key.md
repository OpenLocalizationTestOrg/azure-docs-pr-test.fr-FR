<!--author=SharS last changed: 12/01/15-->

### <a name="step-1-authorize-a-device-toochange-hello-service-data-encryption-key-in-hello-azure-classic-portal"></a>Étape 1 : Autoriser une périphérique toochange hello clé de chiffrement dans hello portail Azure classic
En règle générale, administrateur du périphérique hello demande qu’administrateur de service hello autoriser un clés de chiffrement de données de périphérique toochange service. administrateur de service Hello autorise ensuite clé de hello périphérique toochange hello.

Cette étape est effectuée dans hello portail Azure classic. administrateur de service de Hello peut sélectionner un périphérique dans la liste des périphériques hello qui sont éligible toobe autorisé. Appareil de Hello est le processus de modification de clé de chiffrement de données autorisés toostart hello service.

#### <a name="which-devices-can-be-authorized-toochange-service-data-encryption-keys"></a>Les appareils qui peuvent être autorisés des clés de chiffrement de données de service toochange ?
Un appareil doit respecter hello suivant des critères avant de pouvoir être changements de chiffrement de données service tooinitiate autorisés clés :

* Appareil de Hello doit être en ligne toobe éligible pour l’autorisation de modification de la clé de chiffrement de données service.
* Vous pouvez autoriser hello même périphérique à nouveau après 30 minutes si la modification de la clé de hello n’a pas démarré.
* Vous pouvez autoriser un autre appareil, pour autant que la modification de la clé hello n’a pas été initialisée par périphérique précédemment autorisé de hello. Une fois le nouveau périphérique de hello a été autorisé, hello ancienne ne peut plus lancer les modifications hello.
* Vous ne pouvez pas autoriser un périphérique lors de la substitution de hello de clé de chiffrement de données de service hello est en cours.
* Vous pouvez autoriser un périphérique lorsque certains périphériques hello inscrits avec le service de hello ont annulées via le chiffrement hello tandis que d’autres pas. Dans ce cas, les appareils éligibles hello sont hello ceux qui ont terminé modification clé de chiffrement de données de service de hello.

> [!NOTE]
> Bonjour portail Azure classic, StorSimple périphériques virtuels ne sont pas affichés dans la liste hello des appareils qui peuvent être autorisé de modification de la clé toostart hello.
> 
> 

Effectuer hello suivant les étapes tooselect et autoriser une périphérique tooinitiate hello service chiffrement clé modification de données.

#### <a name="tooauthorize-a-device-toochange-hello-key"></a>tooauthorize une clé de hello toochange périphérique
1. Dans la page de tableau de bord de service hello, cliquez sur **clé de chiffrement de données de service de modification**.
   
    ![Modification de la clé de chiffrement du service](./media/storsimple-change-data-encryption-key/HCS_ChangeServiceDataEncryptionKey-include.png)
2. Bonjour **modification de clé de chiffrement** boîte de dialogue zone et sélectionnez Autoriser une périphérique tooinitiate hello service chiffrement clé modification de données. liste déroulante de Hello a tous les périphériques éligibles hello qui peuvent être autorisés.
3. Cliquez sur une icône de coche hello ![icône en forme de coche](./media/storsimple-change-data-encryption-key/HCS_CheckIcon-include.png).

### <a name="step-2-use-windows-powershell-for-storsimple-tooinitiate-hello-service-data-encryption-key-change"></a>Étape 2 : Utiliser Windows PowerShell pour StorSimple tooinitiate hello service modification chiffrement des données clée
Cette étape s’effectue dans hello Windows PowerShell pour StorSimple interface hello autorisé de l’appareil StorSimple.

> [!NOTE]
> Aucune opération ne peut être effectuées dans hello portail classique Azure de votre service StorSimple Manager avant la fin de la substitution de clé hello.
> 
> 

Si vous utilisez l’interface Windows PowerShell de hello appareil console série tooconnect toohello, effectuer hello comme suit.

#### <a name="tooinitiate-hello-service-data-encryption-key-change"></a>modification de la clé de chiffrement des données tooinitiate hello service
1. Sélectionnez l’option 1 toolog sur avec un accès complet.
2. À l’invite de commandes hello, tapez :
   
     `Invoke-HcsmServiceDataEncryptionKeyChange`
3. Une fois que l’applet de commande hello terminé, vous obtenez une nouvelle clé de chiffrement de données de service. Copiez et enregistrez cette clé pour l’utiliser lors de l’étape 3 de cette procédure. Cette clé sera utilisée tooupdate tous les hello restant appareils inscrits avec le service StorSimple Manager hello.
   
   > [!NOTE]
   > Ce processus doit être démarré dans les quatre heures suivant l’autorisation d’un appareil StorSimple.
   > 
   > 
   
   Cette nouvelle clé est ensuite envoyée toohello toobe envoyée tooall hello périphériques de service qui sont inscrits avec le service de hello. Une alerte apparaîtront dans le tableau de bord de service hello. Hello service désactive toutes les opérations de hello sur les appareils inscrits de hello et administrateur de l’appareil hello puis devez tooupdate hello clé de chiffrement sur hello autres périphériques. Toutefois, hello e/s (hôtes expédiant des données dans le cloud toohello) ne seront pas interrompues.
   
   Si vous avez un seul appareil inscrit tooyour service, les processus de substitution hello sont maintenant terminée et vous pouvez ignorer la prochaine étape de hello. Si vous avez plusieurs service inscrit tooyour de périphériques, passez toostep 3.

### <a name="step-3-update-hello-service-data-encryption-key-on-other-storsimple-devices"></a>Étape 3 : Mettre à jour la clé de chiffrement de données de service hello sur d’autres appareils StorSimple
Ces étapes doivent être effectuées dans l’interface Windows PowerShell de votre appareil StorSimple hello si vous avez plusieurs périphériques inscrits tooyour StorSimple Manager service. clé Hello que vous avez obtenue à l’étape 2 : utiliser Windows PowerShell pour StorSimple tooinitiate hello service données chiffrement modification de la clé doit être utilisé tooupdate tous hello restants de l’appareil StorSimple enregistré avec hello service StorSimple Manager.

Effectuer hello suite de chiffrement de données de service étapes tooupdate hello sur votre appareil.

#### <a name="tooupdate-hello-service-data-encryption-key"></a>clé de chiffrement de données tooupdate hello service
1. Utiliser Windows PowerShell pour StorSimple tooconnect toohello console. Sélectionnez l’option 1 toolog sur avec un accès complet.
2. À l’invite de commandes hello, tapez :
   
    `Invoke-HcsmServiceDataEncryptionKeyChange – ServiceDataEncryptionKey`
3. Fournir hello clé de chiffrement que vous avez obtenue dans [étape 2 : utiliser Windows PowerShell pour StorSimple tooinitiate hello service modification chiffrement des données clée](#to-initiate-the-service-data-encryption-key-change).

