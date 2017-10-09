<!--author=alkohli last changed: 9/16/15-->


#### <a name="toocable-your-device-for-power"></a>toocable votre appareil pour l’alimentation
> [!NOTE]
> Les deux boîtiers sur votre appareil StorSimple incluent des PCM redondants. Pour chaque boîtier, hello PCM doit être installé et connecté toodifferent power sources tooensure haut niveau de disponibilité.
> 
> 

1. Vous assurer que les interrupteurs d’alimentation hello sur tous les hello PCM sont en position OFF de hello.
2. Sur le boîtier principal de hello, se connecter tooboth de câbles d’alimentation hello PCM. cordons d’alimentation Hello sont indiqués en rouge dans hello câblage d’alimentation diagramme, ci-dessous.
3. Vérifiez que hello deux PCM sources d’alimentation distinctes utilisez hello boîtier principal.
4. Attachez hello power câbles toohello mise sous tension hello unités de distribution comme indiqué dans le diagramme de câblage de hello.
5. Répétez les étapes 2 à 4 pour hello boîtiers.
6. Activer les boîtiers hello en interrupteur hello sur chaque position de ON toohello PCM.
7. Vérifiez que hello boîtiers est activé en vérifiant que hello arrière du contrôleur EBOD hello hello vert voyants sont allumés.
8. Allumez le boîtier principal de hello en basculant chaque position de PCM commutateur toohello ON.
9. Vérifiez que le système de hello est sur en veillant à ce contrôleur de l’appareil hello que DEL ont activé.
10. Vérifiez que cette connexion hello entre le contrôleur EBOD hello et contrôleur de l’appareil hello est actif en vérifiant que hello quatre DEL suivant toohello port SAS du contrôleur EBOD hello sont verts.
    
    > [!IMPORTANT]
    > tooensure haute disponibilité pour votre système, nous vous recommandons de respecter strictement toohello les schéma illustré hello suivant schéma de câblage.
    > 
    > 
    
    ![Raccorder votre appareil à l’alimentation électrique](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    **Branchement des câbles d’alimentation**
    
    | Étiquette | Description |
    |:--- |:--- |
    | 1 |Boîtier principal |
    | 2 |PCM 0 |
    | 3 |PCM 1 |
    | 4 |Contrôleur 0 |
    | 5 |Contrôleur 1 |
    | 6 |Contrôleur 0 du boîtier EBOD |
    | 7 |Contrôleur 1 du boîtier EBOD |
    | 8 |Boîtier EBOD |
    | 9 |PDU |

