<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a>tooconnect via la console série de hello
1. Brancher votre câble série toohello (directement ou via un adaptateur USB série).
2. Ouvrez hello **le panneau de configuration**, puis ouvrez hello **le Gestionnaire de périphériques**.
3. Identifiez les ports hello COM comme indiqué dans hello après l’illustration.
   
     ![Connexion via la console série ](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. Démarrez PuTTY. 
5. Dans le volet droit de hello, modifiez hello **type de connexion** trop**série**.
6. Dans le volet droit de hello, tapez le port COM approprié de hello. Assurez-vous que les paramètres de configuration série hello sont définis comme suit :
   
   * Vitesse : 115 200
   * Bits de données : 8
   * Bits d’arrêt : 1
   * Parité : aucune
   * Contrôle de flux : aucun
     
     Ces paramètres sont affichés dans hello après l’illustration.
     
     ![Paramètres puTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > Si le paramètre de contrôle de flux par défaut hello ne fonctionne pas, essayez de définir de contrôle de flux hello tooXON/XOFF.
     > 
     > 
7. Cliquez sur **ouvrir** toostart une session série.

