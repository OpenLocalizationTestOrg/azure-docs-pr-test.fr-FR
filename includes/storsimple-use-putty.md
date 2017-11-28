<!--author=SharS last changed: 9/17/15-->

#### <a name="to-connect-through-the-serial-console"></a><span data-ttu-id="3eb8d-101">Pour établir une connexion via la console série</span><span class="sxs-lookup"><span data-stu-id="3eb8d-101">To connect through the serial console</span></span>
1. <span data-ttu-id="3eb8d-102">Connectez votre câble série à l’appareil (directement ou via un adaptateur USB série).</span><span class="sxs-lookup"><span data-stu-id="3eb8d-102">Connect your serial cable to the device (directly or through a USB-serial adapter).</span></span>
2. <span data-ttu-id="3eb8d-103">Ouvrez le **Panneau de configuration**, puis ouvrez le **Gestionnaire de périphériques**.</span><span class="sxs-lookup"><span data-stu-id="3eb8d-103">Open the **Control Panel**, and then open the **Device Manager**.</span></span>
3. <span data-ttu-id="3eb8d-104">Identifiez le port COM comme indiqué dans l’illustration suivante.</span><span class="sxs-lookup"><span data-stu-id="3eb8d-104">Identify the COM port as shown in the following illustration.</span></span>
   
     ![Connexion via la console série ](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. <span data-ttu-id="3eb8d-106">Démarrez PuTTY.</span><span class="sxs-lookup"><span data-stu-id="3eb8d-106">Start PuTTY.</span></span> 
5. <span data-ttu-id="3eb8d-107">Dans le volet droit, sous **Type de connexion**, cliquez sur **Série**.</span><span class="sxs-lookup"><span data-stu-id="3eb8d-107">In the right pane, change the **Connection type** to **Serial**.</span></span>
6. <span data-ttu-id="3eb8d-108">Dans le volet droit, tapez le port COM approprié.</span><span class="sxs-lookup"><span data-stu-id="3eb8d-108">In the right pane, type the appropriate COM port.</span></span> <span data-ttu-id="3eb8d-109">Assurez-vous que les paramètres de configuration série sont définis comme suit :</span><span class="sxs-lookup"><span data-stu-id="3eb8d-109">Make sure that the serial configuration parameters are set as follows:</span></span>
   
   * <span data-ttu-id="3eb8d-110">Vitesse : 115 200</span><span class="sxs-lookup"><span data-stu-id="3eb8d-110">Speed: 115,200</span></span>
   * <span data-ttu-id="3eb8d-111">Bits de données : 8</span><span class="sxs-lookup"><span data-stu-id="3eb8d-111">Data bits: 8</span></span>
   * <span data-ttu-id="3eb8d-112">Bits d’arrêt : 1</span><span class="sxs-lookup"><span data-stu-id="3eb8d-112">Stop bits: 1</span></span>
   * <span data-ttu-id="3eb8d-113">Parité : aucune</span><span class="sxs-lookup"><span data-stu-id="3eb8d-113">Parity: None</span></span>
   * <span data-ttu-id="3eb8d-114">Contrôle de flux : aucun</span><span class="sxs-lookup"><span data-stu-id="3eb8d-114">Flow control: None</span></span>
     
     <span data-ttu-id="3eb8d-115">Ces paramètres sont affichés dans l’illustration suivante.</span><span class="sxs-lookup"><span data-stu-id="3eb8d-115">These settings are shown in the following illustration.</span></span>
     
     ![Paramètres puTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > <span data-ttu-id="3eb8d-117">Si le contrôle de flux par défaut ne fonctionne pas, essayez de définir le contrôle de flux sur XON/XOFF.</span><span class="sxs-lookup"><span data-stu-id="3eb8d-117">If the default flow control setting does not work, try setting the flow control to XON/XOFF.</span></span>
     > 
     > 
7. <span data-ttu-id="3eb8d-118">Cliquez sur **Ouvrir** pour démarrer une session série.</span><span class="sxs-lookup"><span data-stu-id="3eb8d-118">Click **Open** to start a serial session.</span></span>

