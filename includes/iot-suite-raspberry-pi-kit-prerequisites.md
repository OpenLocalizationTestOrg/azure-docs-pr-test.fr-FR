## <a name="prerequisites"></a><span data-ttu-id="72cf2-101">Composants requis</span><span class="sxs-lookup"><span data-stu-id="72cf2-101">Prerequisites</span></span>

<span data-ttu-id="72cf2-102">toocomplete ce didacticiel, vous avez besoin d’un abonnement Azure actif.</span><span class="sxs-lookup"><span data-stu-id="72cf2-102">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="72cf2-103">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="72cf2-103">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="72cf2-104">Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk-free-trial].</span><span class="sxs-lookup"><span data-stu-id="72cf2-104">For details, see [Azure Free Trial][lnk-free-trial].</span></span>

### <a name="required-software"></a><span data-ttu-id="72cf2-105">Logiciels requis</span><span class="sxs-lookup"><span data-stu-id="72cf2-105">Required software</span></span>

<span data-ttu-id="72cf2-106">Vous devez client SSH sur votre tooenable d’ordinateur de bureau vous tooremotely accès hello de ligne de commande sur hello framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="72cf2-106">You need SSH client on your desktop machine tooenable you tooremotely access hello command line on hello Raspberry Pi.</span></span>

- <span data-ttu-id="72cf2-107">Windows n’inclut pas de client SSH.</span><span class="sxs-lookup"><span data-stu-id="72cf2-107">Windows does not include an SSH client.</span></span> <span data-ttu-id="72cf2-108">Nous vous recommandons d’utiliser [PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="72cf2-108">We recommend using [PuTTY](http://www.putty.org/).</span></span>
- <span data-ttu-id="72cf2-109">La plupart des distributions Linux et Mac OS incluent l’utilitaire SSH hello.</span><span class="sxs-lookup"><span data-stu-id="72cf2-109">Most Linux distributions and Mac OS include hello command-line SSH utility.</span></span> <span data-ttu-id="72cf2-110">Pour plus d’informations, consultez [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (Utilisation de SSH avec Linux ou Mac OS).</span><span class="sxs-lookup"><span data-stu-id="72cf2-110">For more information, see [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).</span></span>

### <a name="required-hardware"></a><span data-ttu-id="72cf2-111">Matériel requis</span><span class="sxs-lookup"><span data-stu-id="72cf2-111">Required hardware</span></span>

<span data-ttu-id="72cf2-112">Un ordinateur de bureau de tooenable vous tooconnect à distance toohello de ligne de commande sur hello framboises Pi.</span><span class="sxs-lookup"><span data-stu-id="72cf2-112">A desktop computer tooenable you tooconnect remotely toohello command line on hello Raspberry Pi.</span></span>

<span data-ttu-id="72cf2-113">[Starter Kit Microsoft IoT pour Raspberry Pi 3][lnk-starter-kits] ou composants équivalents.</span><span class="sxs-lookup"><span data-stu-id="72cf2-113">[Microsoft IoT Starter Kit for Raspberry Pi 3][lnk-starter-kits] or equivalent components.</span></span> <span data-ttu-id="72cf2-114">Ce didacticiel utilise les éléments suivants à partir du kit de hello de hello :</span><span class="sxs-lookup"><span data-stu-id="72cf2-114">This tutorial uses hello following items from hello kit:</span></span>

- <span data-ttu-id="72cf2-115">Raspberry Pi 3</span><span class="sxs-lookup"><span data-stu-id="72cf2-115">Raspberry Pi 3</span></span>
- <span data-ttu-id="72cf2-116">Carte MicroSD (avec NOOBS)</span><span class="sxs-lookup"><span data-stu-id="72cf2-116">MicroSD Card (with NOOBS)</span></span>
- <span data-ttu-id="72cf2-117">Un câble mini USB</span><span class="sxs-lookup"><span data-stu-id="72cf2-117">A USB Mini cable</span></span>
- <span data-ttu-id="72cf2-118">Un câble Ethernet</span><span class="sxs-lookup"><span data-stu-id="72cf2-118">An Ethernet cable</span></span>
- <span data-ttu-id="72cf2-119">Capteur BME280</span><span class="sxs-lookup"><span data-stu-id="72cf2-119">BME280 sensor</span></span>
- <span data-ttu-id="72cf2-120">Platine d’expérimentation</span><span class="sxs-lookup"><span data-stu-id="72cf2-120">Breadboard</span></span>
- <span data-ttu-id="72cf2-121">Câbles de liaison</span><span class="sxs-lookup"><span data-stu-id="72cf2-121">Jumper wires</span></span>
- <span data-ttu-id="72cf2-122">Résistances</span><span class="sxs-lookup"><span data-stu-id="72cf2-122">Resistors</span></span>
- <span data-ttu-id="72cf2-123">LED</span><span class="sxs-lookup"><span data-stu-id="72cf2-123">LEDs</span></span>

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/