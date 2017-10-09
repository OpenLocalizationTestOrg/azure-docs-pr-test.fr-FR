## <a name="build-iot-edge"></a><span data-ttu-id="47b21-101">Générer IoT Edge</span><span class="sxs-lookup"><span data-stu-id="47b21-101">Build IoT Edge</span></span>

<span data-ttu-id="47b21-102">Ce didacticiel utilise toocommunicate de modules personnalisé IoT Edge avec hello solution préconfigurée de surveillance à distance.</span><span class="sxs-lookup"><span data-stu-id="47b21-102">This tutorial uses custom IoT Edge modules toocommunicate with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="47b21-103">Par conséquent, vous devez les modules toobuild hello IoT bord à partir du code source personnalisée.</span><span class="sxs-lookup"><span data-stu-id="47b21-103">Therefore, you need toobuild hello IoT Edge modules from custom source code.</span></span> <span data-ttu-id="47b21-104">Hello les sections suivantes décrire comment tooinstall IoT Edge et build hello module IoT bord personnalisé.</span><span class="sxs-lookup"><span data-stu-id="47b21-104">hello following sections describe how tooinstall IoT Edge and build hello custom IoT Edge module.</span></span>

### <a name="install-iot-edge"></a><span data-ttu-id="47b21-105">Installer IoT Edge</span><span class="sxs-lookup"><span data-stu-id="47b21-105">Install IoT Edge</span></span>

<span data-ttu-id="47b21-106">Hello étapes suivantes décrivent comment tooinstall hello compilé préalable logiciel IoT Edge sur hello Intel NUC :</span><span class="sxs-lookup"><span data-stu-id="47b21-106">hello following steps describe how tooinstall hello pre-compiled IoT Edge software on hello Intel NUC:</span></span>

1. <span data-ttu-id="47b21-107">Configurez les référentiels de package actives hello requis en exécutant les hello suivant de commandes de hello Intel NUC :</span><span class="sxs-lookup"><span data-stu-id="47b21-107">Configure hello required smart package repositories by running hello following commands on hello Intel NUC:</span></span>

    ```bash
    smart channel --add IoT_Cloud type=rpm-md name="IoT_Cloud" baseurl=http://iotdk.intel.com/repos/iot-cloud/wrlinux7/rcpl13/ -y
    smart channel --add WR_Repo type=rpm-md baseurl=https://distro.windriver.com/release/idp-3-xt/public_feeds/WR-IDP-3-XT-Intel-Baytrail-public-repo/RCPL13/corei7_64/
    ```

    <span data-ttu-id="47b21-108">Entrez `y` lorsque hello commande vous demande trop**inclure ce canal ?**.</span><span class="sxs-lookup"><span data-stu-id="47b21-108">Enter `y` when hello command prompts you too**Include this channel?**.</span></span>

1. <span data-ttu-id="47b21-109">Mise à jour hello actives Gestionnaire de package en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="47b21-109">Update hello smart package manager by running hello following command:</span></span>

    ```bash
    smart update
    ```

1. <span data-ttu-id="47b21-110">Installer le package de Azure IoT Edge de hello en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="47b21-110">Install hello Azure IoT Edge package by running hello following command:</span></span>

    ```bash
    smart config --set rpm-check-signatures=false
    smart install packagegroup-cloud-azure -y
    ```

1. <span data-ttu-id="47b21-111">Vérifier l’installation de hello par exemple hello « Hello world ».</span><span class="sxs-lookup"><span data-stu-id="47b21-111">Verify hello installation by running hello "Hello world" sample.</span></span> <span data-ttu-id="47b21-112">Cet exemple écrit un fichier de hello world message toohello log.txT toutes les cinq secondes.</span><span class="sxs-lookup"><span data-stu-id="47b21-112">This sample writes a hello world message toohello log.txT file every five seconds.</span></span> <span data-ttu-id="47b21-113">Hello exécuter les commandes suivantes hello, exemple « Hello world » :</span><span class="sxs-lookup"><span data-stu-id="47b21-113">hello following commands run hello "Hello world" sample:</span></span>

    ```bash
    cd /usr/share/azureiotgatewaysdk/samples/hello_world/
    ./hello_world hello_world.json
    ```

    <span data-ttu-id="47b21-114">Ignorer les **argument non valide** lorsque vous arrêtez l’exemple hello des messages.</span><span class="sxs-lookup"><span data-stu-id="47b21-114">Ignore any **invalid argument** messages when you stop hello sample.</span></span>

    <span data-ttu-id="47b21-115">Utilisez hello suivant le contenu de hello tooview de commande du fichier journal de hello :</span><span class="sxs-lookup"><span data-stu-id="47b21-115">Use hello following command tooview hello contents of hello log file:</span></span>

    ```bash
    cat log.txt | more
    ```

### <a name="troubleshooting"></a><span data-ttu-id="47b21-116">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="47b21-116">Troubleshooting</span></span>

<span data-ttu-id="47b21-117">Si vous recevez une erreur de hello « aucun package ne fournit util-linux-dev », essayez de redémarrer hello NUC d’Intel.</span><span class="sxs-lookup"><span data-stu-id="47b21-117">If you receive hello error "No package provides util-linux-dev", try rebooting hello Intel NUC.</span></span>
