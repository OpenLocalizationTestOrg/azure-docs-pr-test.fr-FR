## <a name="prepare-your-raspberry-pi"></a>Préparer votre Raspberry Pi

### <a name="install-raspbian"></a>Installer Raspbian

S’il s’agit hello première fois que vous utilisez votre Pi framboises, vous devez tooinstall hello Raspbian système d’exploitation NOOBS sur la carte SD de hello inclus dans le kit de hello. Hello [framboises Pi logiciel Guide] [ lnk-install-raspbian] décrit comment tooinstall un système d’exploitation sur votre Pi framboises. Ce didacticiel suppose que vous avez installé le système d’exploitation de Raspbian hello sur votre Pi framboises.

> [!NOTE]
> carte SD de Hello inclus dans hello [Microsoft Azure IoT Starter Kit pour framboises Pi 3] [ lnk-starter-kits] a déjà NOOBS installé. Vous pouvez démarrer hello framboises Pi à partir de cette carte et choisissez tooinstall hello Raspbian du système d’exploitation.

le programme d’installation matérielle hello toocomplete, vous devez :

- Connectez l’alimentation framboises Pi toohello incluse dans le kit de hello.
- Connecter votre réseau de tooyour framboises Pi à l’aide d’un câble Ethernet hello inclus dans le kit de. Vous pouvez également configurer [Connectivité sans fil][lnk-pi-wireless] pour votre Raspberry Pi.

Vous avez maintenant terminé la configuration du matériel de votre Pi framboises hello.

### <a name="sign-in-and-access-hello-terminal"></a>Se connecter et accéder à Terminal Server de hello

Vous avez deux options tooaccess d’un environnement de Terminal Server sur votre Pi framboises :

- Si vous possédez un clavier et surveillez tooyour connecté framboises Pi, vous pouvez utiliser hello Raspbian GUI tooaccess une fenêtre de terminal.

- Ligne de commande accès hello sur votre Pi framboises à l’aide de SSH à partir de votre ordinateur de bureau.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Utiliser une fenêtre de terminal dans l’interface graphique utilisateur de hello

informations d’identification par défaut de Hello pour Raspbian sont le nom d’utilisateur **pi** et le mot de passe **framboises**. Dans la barre des tâches hello Bonjour l’interface graphique utilisateur, vous pouvez lancer hello **Terminal** utility à l’aide d’icône hello qui ressemble à une analyse.

#### <a name="sign-in-with-ssh"></a>Se connecter avec SSH

Vous pouvez utiliser SSH pour l’accès en ligne de commande tooyour framboises Pi. article de Hello [SSH (Secure Shell)] [ lnk-pi-ssh] décrit comment tooconfigure SSH sur votre Pi framboises et comment tooconnect de [Windows] [ lnk-ssh-windows] ou [Linux et Mac OS][lnk-ssh-linux].

Connectez-vous avec le nom d’utilisateur **pi** et le mot de passe **raspberry**.

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a>Facultatif : partager un dossier sur votre Raspberry Pi

Si vous le souhaitez, vous souhaiterez tooshare un dossier sur votre Pi framboises avec votre environnement de bureau. Partage d’un dossier permet de vous toouse votre éditeur de texte de bureau par défaut (tel que [Visual Studio Code](https://code.visualstudio.com/) ou [texte Sublime](http://www.sublimetext.com/)) tooedit des fichiers sur votre Pi framboises au lieu d’utiliser `nano` ou `vi`.

tooshare un dossier avec Windows, configurez un serveur Samba sur hello framboises Pi. Vous pouvez également utiliser intégrée de hello [SFTP](https://www.raspberrypi.org/documentation/remote-access/) serveur avec un client SFTP sur votre bureau.

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/