## <a name="prepare-your-raspberry-pi"></a><span data-ttu-id="40511-101">Préparer votre Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="40511-101">Prepare your Raspberry Pi</span></span>

### <a name="install-raspbian"></a><span data-ttu-id="40511-102">Installer Raspbian</span><span class="sxs-lookup"><span data-stu-id="40511-102">Install Raspbian</span></span>

<span data-ttu-id="40511-103">S’il s’agit hello première fois que vous utilisez votre Pi framboises, vous devez tooinstall hello Raspbian système d’exploitation NOOBS sur la carte SD de hello inclus dans le kit de hello.</span><span class="sxs-lookup"><span data-stu-id="40511-103">If this is hello first time you are using your Raspberry Pi, you need tooinstall hello Raspbian operating system using NOOBS on hello SD card included in hello kit.</span></span> <span data-ttu-id="40511-104">Hello [framboises Pi logiciel Guide] [ lnk-install-raspbian] décrit comment tooinstall un système d’exploitation sur votre Pi framboises.</span><span class="sxs-lookup"><span data-stu-id="40511-104">hello [Raspberry Pi Software Guide][lnk-install-raspbian] describes how tooinstall an operating system on your Raspberry Pi.</span></span> <span data-ttu-id="40511-105">Ce didacticiel suppose que vous avez installé le système d’exploitation de Raspbian hello sur votre Pi framboises.</span><span class="sxs-lookup"><span data-stu-id="40511-105">This tutorial assumes you have installed hello Raspbian operating system on your Raspberry Pi.</span></span>

> [!NOTE]
> <span data-ttu-id="40511-106">carte SD de Hello inclus dans hello [Microsoft Azure IoT Starter Kit pour framboises Pi 3] [ lnk-starter-kits] a déjà NOOBS installé.</span><span class="sxs-lookup"><span data-stu-id="40511-106">hello SD card included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] already has NOOBS installed.</span></span> <span data-ttu-id="40511-107">Vous pouvez démarrer hello framboises Pi à partir de cette carte et choisissez tooinstall hello Raspbian du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="40511-107">You can boot hello Raspberry Pi from this card and choose tooinstall hello Raspbian OS.</span></span>

### <a name="set-up-hello-hardware"></a><span data-ttu-id="40511-108">Configurer le matériel de hello</span><span class="sxs-lookup"><span data-stu-id="40511-108">Set up hello hardware</span></span>

<span data-ttu-id="40511-109">Ce didacticiel utilise capteur hello BME280 inclus dans hello [Microsoft Azure IoT Starter Kit pour framboises Pi 3] [ lnk-starter-kits] toogenerate les données de télémétrie.</span><span class="sxs-lookup"><span data-stu-id="40511-109">This tutorial uses hello BME280 sensor included in hello [Microsoft Azure IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] toogenerate telemetry data.</span></span> <span data-ttu-id="40511-110">Elle utilise un tooindicate LED lorsque hello framboises Pi traite un appel de méthode à partir du tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="40511-110">It uses an LED tooindicate when hello Raspberry Pi processes a method invocation from hello solution dashboard.</span></span>

<span data-ttu-id="40511-111">composants Hello sur la carte de pain hello sont :</span><span class="sxs-lookup"><span data-stu-id="40511-111">hello components on hello bread board are:</span></span>

- <span data-ttu-id="40511-112">LED rouge</span><span class="sxs-lookup"><span data-stu-id="40511-112">Red LED</span></span>
- <span data-ttu-id="40511-113">Résistance de 220 ohms (rouge, marron)</span><span class="sxs-lookup"><span data-stu-id="40511-113">220-Ohm resistor (red, red, brown)</span></span>
- <span data-ttu-id="40511-114">Capteur BME280</span><span class="sxs-lookup"><span data-stu-id="40511-114">BME280 sensor</span></span>

<span data-ttu-id="40511-115">diagramme Hello suivant montre comment tooconnect votre matériel :</span><span class="sxs-lookup"><span data-stu-id="40511-115">hello following diagram shows how tooconnect your hardware:</span></span>

![Configuration matérielle de Raspberry Pi][img-connection-diagram]

<span data-ttu-id="40511-117">Hello tableau suivant résume les connexions à partir des composants de toohello framboises Pi hello sur breadboard de hello hello :</span><span class="sxs-lookup"><span data-stu-id="40511-117">hello following table summarizes hello connections from hello Raspberry Pi toohello components on hello breadboard:</span></span>

| <span data-ttu-id="40511-118">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="40511-118">Raspberry Pi</span></span>            | <span data-ttu-id="40511-119">Platine d’expérimentation</span><span class="sxs-lookup"><span data-stu-id="40511-119">Breadboard</span></span>             |<span data-ttu-id="40511-120">Couleur</span><span class="sxs-lookup"><span data-stu-id="40511-120">Color</span></span>         |
| ----------------------- | ---------------------- | ------------- |
| <span data-ttu-id="40511-121">GND (broche 14)</span><span class="sxs-lookup"><span data-stu-id="40511-121">GND (Pin 14)</span></span>            | <span data-ttu-id="40511-122">Broche à LED (18 A)</span><span class="sxs-lookup"><span data-stu-id="40511-122">LED -ve pin (18A)</span></span>      | <span data-ttu-id="40511-123">Violet</span><span class="sxs-lookup"><span data-stu-id="40511-123">Purple</span></span>          |
| <span data-ttu-id="40511-124">GPCLK0 (broche 7)</span><span class="sxs-lookup"><span data-stu-id="40511-124">GPCLK0 (Pin 7)</span></span>          | <span data-ttu-id="40511-125">Résistance (25 A)</span><span class="sxs-lookup"><span data-stu-id="40511-125">Resistor (25A)</span></span>         | <span data-ttu-id="40511-126">Orange</span><span class="sxs-lookup"><span data-stu-id="40511-126">Orange</span></span>          |
| <span data-ttu-id="40511-127">SPI_CE0 (broche 24)</span><span class="sxs-lookup"><span data-stu-id="40511-127">SPI_CE0 (Pin 24)</span></span>        | <span data-ttu-id="40511-128">CS (39 A)</span><span class="sxs-lookup"><span data-stu-id="40511-128">CS (39A)</span></span>               | <span data-ttu-id="40511-129">Bleu</span><span class="sxs-lookup"><span data-stu-id="40511-129">Blue</span></span>          |
| <span data-ttu-id="40511-130">SPI_SCLK (broche 23)</span><span class="sxs-lookup"><span data-stu-id="40511-130">SPI_SCLK (Pin 23)</span></span>       | <span data-ttu-id="40511-131">SCK (36 A)</span><span class="sxs-lookup"><span data-stu-id="40511-131">SCK (36A)</span></span>              | <span data-ttu-id="40511-132">Jaune</span><span class="sxs-lookup"><span data-stu-id="40511-132">Yellow</span></span>        |
| <span data-ttu-id="40511-133">SPI_MISO (broche 21)</span><span class="sxs-lookup"><span data-stu-id="40511-133">SPI_MISO (Pin 21)</span></span>       | <span data-ttu-id="40511-134">SDO (37 A)</span><span class="sxs-lookup"><span data-stu-id="40511-134">SDO (37A)</span></span>              | <span data-ttu-id="40511-135">Blanc</span><span class="sxs-lookup"><span data-stu-id="40511-135">White</span></span>         |
| <span data-ttu-id="40511-136">SPI_MOSI (broche 19)</span><span class="sxs-lookup"><span data-stu-id="40511-136">SPI_MOSI (Pin 19)</span></span>       | <span data-ttu-id="40511-137">SDI (38 A)</span><span class="sxs-lookup"><span data-stu-id="40511-137">SDI (38A)</span></span>              | <span data-ttu-id="40511-138">Vert</span><span class="sxs-lookup"><span data-stu-id="40511-138">Green</span></span>         |
| <span data-ttu-id="40511-139">GND (broche 6)</span><span class="sxs-lookup"><span data-stu-id="40511-139">GND (Pin 6)</span></span>             | <span data-ttu-id="40511-140">GND (35 A)</span><span class="sxs-lookup"><span data-stu-id="40511-140">GND (35A)</span></span>              | <span data-ttu-id="40511-141">Noir</span><span class="sxs-lookup"><span data-stu-id="40511-141">Black</span></span>         |
| <span data-ttu-id="40511-142">3,3 V (broche 1)</span><span class="sxs-lookup"><span data-stu-id="40511-142">3.3 V (Pin 1)</span></span>           | <span data-ttu-id="40511-143">3Vo (34 A)</span><span class="sxs-lookup"><span data-stu-id="40511-143">3Vo (34A)</span></span>              | <span data-ttu-id="40511-144">Rouge</span><span class="sxs-lookup"><span data-stu-id="40511-144">Red</span></span>           |

<span data-ttu-id="40511-145">le programme d’installation matérielle hello toocomplete, vous devez :</span><span class="sxs-lookup"><span data-stu-id="40511-145">toocomplete hello hardware setup, you need to:</span></span>

- <span data-ttu-id="40511-146">Connectez l’alimentation framboises Pi toohello incluse dans le kit de hello.</span><span class="sxs-lookup"><span data-stu-id="40511-146">Connect your Raspberry Pi toohello power supply included in hello kit.</span></span>
- <span data-ttu-id="40511-147">Connecter votre réseau de tooyour framboises Pi à l’aide d’un câble Ethernet hello inclus dans le kit de.</span><span class="sxs-lookup"><span data-stu-id="40511-147">Connect your Raspberry Pi tooyour network using hello Ethernet cable included in your kit.</span></span> <span data-ttu-id="40511-148">Vous pouvez également configurer [Connectivité sans fil][lnk-pi-wireless] pour votre Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="40511-148">Alternatively, you can set up [Wireless Connectivity][lnk-pi-wireless] for your Raspberry Pi.</span></span>

<span data-ttu-id="40511-149">Vous avez maintenant terminé la configuration du matériel de votre Pi framboises hello.</span><span class="sxs-lookup"><span data-stu-id="40511-149">You have now completed hello hardware setup of your Raspberry Pi.</span></span>

### <a name="sign-in-and-access-hello-terminal"></a><span data-ttu-id="40511-150">Se connecter et accéder à Terminal Server de hello</span><span class="sxs-lookup"><span data-stu-id="40511-150">Sign in and access hello terminal</span></span>

<span data-ttu-id="40511-151">Vous avez deux options tooaccess d’un environnement de Terminal Server sur votre Pi framboises :</span><span class="sxs-lookup"><span data-stu-id="40511-151">You have two options tooaccess a terminal environment on your Raspberry Pi:</span></span>

- <span data-ttu-id="40511-152">Si vous possédez un clavier et surveillez tooyour connecté framboises Pi, vous pouvez utiliser hello Raspbian GUI tooaccess une fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="40511-152">If you have a keyboard and monitor connected tooyour Raspberry Pi, you can use hello Raspbian GUI tooaccess a terminal window.</span></span>

- <span data-ttu-id="40511-153">Ligne de commande accès hello sur votre Pi framboises à l’aide de SSH à partir de votre ordinateur de bureau.</span><span class="sxs-lookup"><span data-stu-id="40511-153">Access hello command line on your Raspberry Pi using SSH from your desktop machine.</span></span>

#### <a name="use-a-terminal-window-in-hello-gui"></a><span data-ttu-id="40511-154">Utiliser une fenêtre de terminal dans l’interface graphique utilisateur de hello</span><span class="sxs-lookup"><span data-stu-id="40511-154">Use a terminal Window in hello GUI</span></span>

<span data-ttu-id="40511-155">informations d’identification par défaut de Hello pour Raspbian sont le nom d’utilisateur **pi** et le mot de passe **framboises**.</span><span class="sxs-lookup"><span data-stu-id="40511-155">hello default credentials for Raspbian are username **pi** and password **raspberry**.</span></span> <span data-ttu-id="40511-156">Dans la barre des tâches hello Bonjour l’interface graphique utilisateur, vous pouvez lancer hello **Terminal** utility à l’aide d’icône hello qui ressemble à une analyse.</span><span class="sxs-lookup"><span data-stu-id="40511-156">In hello task bar in hello GUI, you can launch hello **Terminal** utility using hello icon that looks like a monitor.</span></span>

#### <a name="sign-in-with-ssh"></a><span data-ttu-id="40511-157">Se connecter avec SSH</span><span class="sxs-lookup"><span data-stu-id="40511-157">Sign in with SSH</span></span>

<span data-ttu-id="40511-158">Vous pouvez utiliser SSH pour l’accès en ligne de commande tooyour framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="40511-158">You can use SSH for command-line access tooyour Raspberry Pi.</span></span> <span data-ttu-id="40511-159">article de Hello [SSH (Secure Shell)] [ lnk-pi-ssh] décrit comment tooconfigure SSH sur votre Pi framboises et comment tooconnect de [Windows] [ lnk-ssh-windows] ou [Linux et Mac OS][lnk-ssh-linux].</span><span class="sxs-lookup"><span data-stu-id="40511-159">hello article [SSH (Secure Shell)][lnk-pi-ssh] describes how tooconfigure SSH on your Raspberry Pi, and how tooconnect from [Windows][lnk-ssh-windows] or [Linux & Mac OS][lnk-ssh-linux].</span></span>

<span data-ttu-id="40511-160">Connectez-vous avec le nom d’utilisateur **pi** et le mot de passe **raspberry**.</span><span class="sxs-lookup"><span data-stu-id="40511-160">Sign in with username **pi** and password **raspberry**.</span></span>

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a><span data-ttu-id="40511-161">Facultatif : partager un dossier sur votre Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="40511-161">Optional: Share a folder on your Raspberry Pi</span></span>

<span data-ttu-id="40511-162">Si vous le souhaitez, vous souhaiterez tooshare un dossier sur votre Pi framboises avec votre environnement de bureau.</span><span class="sxs-lookup"><span data-stu-id="40511-162">Optionally, you may want tooshare a folder on your Raspberry Pi with your desktop environment.</span></span> <span data-ttu-id="40511-163">Partage d’un dossier permet de vous toouse votre éditeur de texte de bureau par défaut (tel que [Visual Studio Code](https://code.visualstudio.com/) ou [texte Sublime](http://www.sublimetext.com/)) tooedit des fichiers sur votre Pi framboises au lieu d’utiliser `nano` ou `vi`.</span><span class="sxs-lookup"><span data-stu-id="40511-163">Sharing a folder enables you toouse your preferred desktop text editor (such as [Visual Studio Code](https://code.visualstudio.com/) or [Sublime Text](http://www.sublimetext.com/)) tooedit files on your Raspberry Pi instead of using `nano` or `vi`.</span></span>

<span data-ttu-id="40511-164">tooshare un dossier avec Windows, configurez un serveur Samba sur hello framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="40511-164">tooshare a folder with Windows, configure a Samba server on hello Raspberry Pi.</span></span> <span data-ttu-id="40511-165">Vous pouvez également utiliser intégrée de hello [SFTP](https://www.raspberrypi.org/documentation/remote-access/) serveur avec un client SFTP sur votre bureau.</span><span class="sxs-lookup"><span data-stu-id="40511-165">Alternatively, use hello built-in [SFTP](https://www.raspberrypi.org/documentation/remote-access/) server with an SFTP client on your desktop.</span></span>

### <a name="enable-spi"></a><span data-ttu-id="40511-166">Activer SPI</span><span class="sxs-lookup"><span data-stu-id="40511-166">Enable SPI</span></span>

<span data-ttu-id="40511-167">Vous pouvez exécuter l’exemple d’application hello, vous devez activer bus Interface périphériques série (SPI) hello hello framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="40511-167">Before you can run hello sample application, you must enable hello Serial Peripheral Interface (SPI) bus on hello Raspberry Pi.</span></span> <span data-ttu-id="40511-168">Hello framboises Pi communique avec un dispositif de capteur BME280 hello sur hello bus SPI.</span><span class="sxs-lookup"><span data-stu-id="40511-168">hello Raspberry Pi communicates with hello BME280 sensor device over hello SPI bus.</span></span> <span data-ttu-id="40511-169">Utilisez hello le fichier de configuration de commande tooedit hello suivant :</span><span class="sxs-lookup"><span data-stu-id="40511-169">Use hello following command tooedit hello configuration file:</span></span>

```sh
sudo nano /boot/config.txt
```

<span data-ttu-id="40511-170">Recherchez hello ligne :</span><span class="sxs-lookup"><span data-stu-id="40511-170">Find hello line:</span></span>

`#dtparam=spi=on`

- <span data-ttu-id="40511-171">ligne de hello toouncomment, delete hello `#` au début de hello.</span><span class="sxs-lookup"><span data-stu-id="40511-171">toouncomment hello line, delete hello `#` at hello start.</span></span>
- <span data-ttu-id="40511-172">Enregistrez vos modifications (**Ctrl-O**, **entrée**) et quittez l’éditeur hello (**Ctrl-X**).</span><span class="sxs-lookup"><span data-stu-id="40511-172">Save your changes (**Ctrl-O**, **Enter**) and exit hello editor (**Ctrl-X**).</span></span>
- <span data-ttu-id="40511-173">tooenable SPI, redémarrez hello framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="40511-173">tooenable SPI, reboot hello Raspberry Pi.</span></span> <span data-ttu-id="40511-174">Redémarrage déconnecte terminal de hello, vous avez besoin toosign de nouveau au redémarrage de hello framboises Pi :</span><span class="sxs-lookup"><span data-stu-id="40511-174">Rebooting disconnects hello terminal, you need toosign in again when hello Raspberry Pi restarts:</span></span>

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