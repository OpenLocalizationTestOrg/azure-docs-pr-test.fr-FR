## <a name="overview"></a><span data-ttu-id="cf7a0-101">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="cf7a0-101">Overview</span></span>

<span data-ttu-id="cf7a0-102">Dans ce didacticiel, vous effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="cf7a0-102">In this tutorial, you complete hello following steps:</span></span>

- <span data-ttu-id="cf7a0-103">Déployer une instance de hello distant tooyour solution préconfigurée analyse abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="cf7a0-103">Deploy an instance of hello remote monitoring preconfigured solution tooyour Azure subscription.</span></span> <span data-ttu-id="cf7a0-104">Cette étape déploie et configure automatiquement plusieurs services Azure.</span><span class="sxs-lookup"><span data-stu-id="cf7a0-104">This step automatically deploys and configures multiple Azure services.</span></span>
- <span data-ttu-id="cf7a0-105">Configurer votre toocommunicate de périphérique avec votre ordinateur et de la solution d’analyse à distance hello.</span><span class="sxs-lookup"><span data-stu-id="cf7a0-105">Set up your device toocommunicate with your computer and hello remote monitoring solution.</span></span>
- <span data-ttu-id="cf7a0-106">Hello exemple périphérique code tooconnect toohello distant solution d’analyse de mise à jour et envoyer la télémétrie simulée que vous pouvez afficher sur le tableau de bord de solution hello.</span><span class="sxs-lookup"><span data-stu-id="cf7a0-106">Update hello sample device code tooconnect toohello remote monitoring solution, and send simulated telemetry that you can view on hello solution dashboard.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf7a0-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cf7a0-107">Prerequisites</span></span>

<span data-ttu-id="cf7a0-108">toocomplete ce didacticiel, vous avez besoin d’un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="cf7a0-108">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="cf7a0-109">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="cf7a0-109">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="cf7a0-110">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="cf7a0-110">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="cf7a0-111">Logiciels requis</span><span class="sxs-lookup"><span data-stu-id="cf7a0-111">Required software</span></span>

<span data-ttu-id="cf7a0-112">Vous devez client SSH sur votre tooenable d’ordinateur de bureau vous tooremotely accès hello de ligne de commande sur hello framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="cf7a0-112">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="cf7a0-113">Windows n’inclut pas de client SSH.</span><span class="sxs-lookup"><span data-stu-id="cf7a0-113">Windows does not include an SSH client.</span></span> <span data-ttu-id="cf7a0-114">Nous vous recommandons d’utiliser [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="cf7a0-114">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="cf7a0-115">La plupart des distributions Linux et Mac OS incluent l’utilitaire SSH hello.</span><span class="sxs-lookup"><span data-stu-id="cf7a0-115">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="cf7a0-116">Pour plus d’informations, consultez [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (Utilisation de SSH avec Linux ou Mac OS).</span><span class="sxs-lookup"><span data-stu-id="cf7a0-116">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="cf7a0-117">Matériel requis</span><span class="sxs-lookup"><span data-stu-id="cf7a0-117">Required hardware</span></span>

<span data-ttu-id="cf7a0-118">Un ordinateur de bureau de tooenable vous tooconnect à distance toohello de ligne de commande sur hello framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="cf7a0-118">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="cf7a0-119">[Starter Kit Microsoft IoT pour Raspberry Pi 3][lnk-starter-kits] ou composants équivalents.</span><span class="sxs-lookup"><span data-stu-id="cf7a0-119">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="cf7a0-120">Ce didacticiel utilise les éléments suivants à partir du kit de hello de hello :</span><span class="sxs-lookup"><span data-stu-id="cf7a0-120">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="cf7a0-121">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="cf7a0-121">Raspberry Pi 3</span></span>
- <span data-ttu-id="cf7a0-122">Carte MicroSD (avec NOOBS)</span><span class="sxs-lookup"><span data-stu-id="cf7a0-122">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="cf7a0-123">Un câble mini USB</span><span class="sxs-lookup"><span data-stu-id="cf7a0-123">A USB Mini cable</span></span>
- <span data-ttu-id="cf7a0-124">Un câble Ethernet</span><span class="sxs-lookup"><span data-stu-id="cf7a0-124">An Ethernet cable</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/