<!--author=SharS last changed: 9/17/15-->

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, initialiser et formater un volume
1. Démarrez l’initiateur iSCSI Microsoft hello.
2. Bonjour **propriétés de l’initiateur iSCSI** fenêtre hello **découverte** , cliquez sur **découvrir un portail**.
3. Bonjour **détecter un portail cible** boîte de dialogue, fournir l’adresse IP de hello de votre interface réseau iSCSI, puis cliquez sur **OK**. 
4. Bonjour **propriétés de l’initiateur iSCSI** fenêtre hello **cibles** localiser hello, onglet **découverts cibles**. état du périphérique Hello doit apparaître en tant que **inactif**.
5. Sélectionnez l’appareil cible de hello, puis cliquez **connexion**. Une fois hello est connecté, état de hello doit également modifier**connecté**. (Pour plus d’informations sur l’utilisation de l’initiateur iSCSI Microsoft hello, consultez [installation et configuration de Microsoft iSCSI Initiator][1]).
6. Sur votre hôte Windows, appuyez sur la touche de Logo Windows hello + X, puis cliquez sur **exécuter**. 
7. Bonjour **exécuter** boîte de dialogue, tapez **Diskmgmt.msc**. Cliquez sur **OK**et hello **gestion des disques** boîte de dialogue s’affiche. volet de droite Hello affichera les volumes hello sur votre ordinateur hôte.
8. Bonjour **gestion des disques** fenêtre hello volumes montés s’affichent comme illustré hello après l’illustration. Cliquez sur hello découverts volume (cliquez sur le nom du disque hello), puis cliquez sur **Online**.
   
     ![Initialisation du formatage de volume](./media/storsimple-mount-initialize-format-volume/HCS_InitializeFormatVolume-include.png) 
9. Cliquez sur hello volume (cliquez sur le nom du disque hello), puis cliquez sur **initialiser**.
10. tooformat un volume simple, effectuez hello comme suit :
    
    1. Sélectionnez le volume hello, faites un clic droit (cliquez sur la zone de droite hello), puis cliquez sur **nouveau Volume Simple**.
    2. Dans l’Assistant Nouveau Volume Simple de hello, spécifiez la lettre de lecteur et de la taille du volume hello et de configurer le volume hello en tant que système de fichiers NTFS.
    3. Spécifiez une taille d’unité d’allocation 64 Ko. Cette taille d’unité d’allocation fonctionne bien avec les algorithmes de déduplication hello utilisés Bonjour solution StorSimple.
    4. Effectuez un formatage rapide.

![Vidéo disponible](./media/storsimple-mount-initialize-format-volume/Video_icon.png)**Vidéo disponible**

toowatch une vidéo qui montre comment toomount, initialiser et formatez un volume StorSimple, cliquez sur [ici](https://azure.microsoft.com/documentation/videos/mount-initialize-and-format-a-storsimple-volume/).

<!--Link references-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx
