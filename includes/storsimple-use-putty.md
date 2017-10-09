<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a><span data-ttu-id="0920b-101">tooconnect via la console série de hello</span><span class="sxs-lookup"><span data-stu-id="0920b-101">tooconnect through hello serial console</span></span>
1. <span data-ttu-id="0920b-102">Brancher votre câble série toohello (directement ou via un adaptateur USB série).</span><span class="sxs-lookup"><span data-stu-id="0920b-102">Connect your serial cable toohello device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="0920b-103">Ouvrez hello **le panneau de configuration**, puis ouvrez hello **le Gestionnaire de périphériques**.</span><span class="sxs-lookup"><span data-stu-id="0920b-103">Open hello **Control Panel**, and then open hello **Device Manager**.</span></span>
3. <span data-ttu-id="0920b-104">Identifiez les ports hello COM comme indiqué dans hello après l’illustration.</span><span class="sxs-lookup"><span data-stu-id="0920b-104">Identify hello COM port as shown in hello following illustration.</span></span>
   
     ![Connexion via la console série ](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="0920b-106">Démarrez PuTTY.</span><span class="sxs-lookup"><span data-stu-id="0920b-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="0920b-107">Dans le volet droit de hello, modifiez hello **type de connexion** trop**série**.</span><span class="sxs-lookup"><span data-stu-id="0920b-107">In hello right pane, change hello **Connection type** too**Serial**.</span></span>
6. <span data-ttu-id="0920b-108">Dans le volet droit de hello, tapez le port COM approprié de hello.</span><span class="sxs-lookup"><span data-stu-id="0920b-108">In hello right pane, type hello appropriate COM port.</span></span> <span data-ttu-id="0920b-109">Assurez-vous que les paramètres de configuration série hello sont définis comme suit :</span><span class="sxs-lookup"><span data-stu-id="0920b-109">Make sure that hello serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="0920b-110">Vitesse : 115 200</span><span class="sxs-lookup"><span data-stu-id="0920b-110">Speed: 115,200</span></span>
   * <span data-ttu-id="0920b-111">Bits de données : 8</span><span class="sxs-lookup"><span data-stu-id="0920b-111">Data bits: 8</span></span>
   * <span data-ttu-id="0920b-112">Bits d’arrêt : 1</span><span class="sxs-lookup"><span data-stu-id="0920b-112">Stop bits: 1</span></span>
   * <span data-ttu-id="0920b-113">Parité : aucune</span><span class="sxs-lookup"><span data-stu-id="0920b-113">Parity: None</span></span>
   * <span data-ttu-id="0920b-114">Contrôle de flux : aucun</span><span class="sxs-lookup"><span data-stu-id="0920b-114">Flow control: None</span></span>
     
     <span data-ttu-id="0920b-115">Ces paramètres sont affichés dans hello après l’illustration.</span><span class="sxs-lookup"><span data-stu-id="0920b-115">These settings are shown in hello following illustration.</span></span>
     
     ![Paramètres puTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="0920b-117">Si le paramètre de contrôle de flux par défaut hello ne fonctionne pas, essayez de définir de contrôle de flux hello tooXON/XOFF.</span><span class="sxs-lookup"><span data-stu-id="0920b-117">If hello default flow control setting does not work, try setting hello flow control tooXON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="0920b-118">Cliquez sur **ouvrir** toostart une session série.</span><span class="sxs-lookup"><span data-stu-id="0920b-118">Click **Open** toostart a serial session.</span></span>

