## <a name="prepare-your-raspberry-pi"></a>Préparer votre Raspberry Pi

### <a name="install-raspbian"></a>Installer Raspbian

S’il s’agit hello première fois que vous utilisez votre Pi framboises, vous devez tooinstall hello Raspbian système d’exploitation NOOBS sur la carte SD de hello inclus dans le kit de hello. Hello [framboises Pi logiciel Guide] [ lnk-install-raspbian] décrit comment tooinstall un système d’exploitation sur votre Pi framboises. Ce didacticiel suppose que vous avez installé le système d’exploitation de Raspbian hello sur votre Pi framboises.

> [!NOTE]
> carte SD de Hello inclus dans hello [Microsoft Azure IoT Starter Kit pour framboises Pi 3] [ lnk-starter-kits] a déjà NOOBS installé. Vous pouvez démarrer hello framboises Pi à partir de cette carte et choisissez tooinstall hello Raspbian du système d’exploitation.

### <a name="set-up-hello-hardware"></a>Configurer le matériel de hello

Ce didacticiel utilise capteur hello BME280 inclus dans hello [Microsoft Azure IoT Starter Kit pour framboises Pi 3] [ lnk-starter-kits] toogenerate les données de télémétrie. Elle utilise un tooindicate LED lorsque hello framboises Pi traite un appel de méthode à partir du tableau de bord de solution hello.

composants Hello sur la carte de pain hello sont :

- LED rouge
- Résistance de 220 ohms (rouge, marron)
- Capteur BME280

diagramme Hello suivant montre comment tooconnect votre matériel :

![Configuration matérielle de Raspberry Pi][img-connection-diagram]

Hello tableau suivant résume les connexions à partir des composants de toohello framboises Pi hello sur breadboard de hello hello :

| Raspberry Pi            | Platine d’expérimentation             |Couleur         |
| ----------------------- | ---------------------- | ------------- |
| GND (broche 14)            | Broche à LED (18 A)      | Violet          |
| GPCLK0 (broche 7)          | Résistance (25 A)         | Orange          |
| SPI_CE0 (broche 24)        | CS (39 A)               | Bleu          |
| SPI_SCLK (broche 23)       | SCK (36 A)              | Jaune        |
| SPI_MISO (broche 21)       | SDO (37 A)              | Blanc         |
| SPI_MOSI (broche 19)       | SDI (38 A)              | Vert         |
| GND (broche 6)             | GND (35 A)              | Noir         |
| 3,3 V (broche 1)           | 3Vo (34 A)              | Rouge           |

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

### <a name="enable-spi"></a>Activer SPI

Vous pouvez exécuter l’exemple d’application hello, vous devez activer bus Interface périphériques série (SPI) hello hello framboises Pi. Hello framboises Pi communique avec un dispositif de capteur BME280 hello sur hello bus SPI. Utilisez hello le fichier de configuration de commande tooedit hello suivant :

```sh
sudo nano /boot/config.txt
```

Recherchez hello ligne :

`#dtparam=spi=on`

- ligne de hello toouncomment, delete hello `#` au début de hello.
- Enregistrez vos modifications (**Ctrl-O**, **entrée**) et quittez l’éditeur hello (**Ctrl-X**).
- tooenable SPI, redémarrez hello framboises Pi. Redémarrage déconnecte terminal de hello, vous avez besoin toosign de nouveau au redémarrage de hello framboises Pi :

  ```sh
  sudo reboot
  ```


[img-connection-diagram]: media/iot-suite-raspberry-pi-kit-prepare-pi/rpi2_remote_monitoring.png

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/