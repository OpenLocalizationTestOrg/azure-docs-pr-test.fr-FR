<!--author=SharS last changed: 9/17/15-->

#### <a name="tooinstall-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="4f51d-101">correctifs normaux de tooinstall via Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="4f51d-101">tooinstall regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="4f51d-102">Connecter la console série du périphérique toohello.</span><span class="sxs-lookup"><span data-stu-id="4f51d-102">Connect toohello device serial console.</span></span> <span data-ttu-id="4f51d-103">Pour plus d’informations, consultez [étape 1 : connecter la console série de toohello](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="4f51d-103">For more information, see [Step 1: Connect toohello serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="4f51d-104">Dans le menu de console série hello, sélectionnez l’option 1, **connecter avec un accès complet**.</span><span class="sxs-lookup"><span data-stu-id="4f51d-104">In hello serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="4f51d-105">Mot de passe type hello.</span><span class="sxs-lookup"><span data-stu-id="4f51d-105">Type hello password.</span></span> <span data-ttu-id="4f51d-106">mot de passe Hello **Password1**.</span><span class="sxs-lookup"><span data-stu-id="4f51d-106">hello default password is **Password1**.</span></span>
3. <span data-ttu-id="4f51d-107">À l’invite de commandes hello, tapez :</span><span class="sxs-lookup"><span data-stu-id="4f51d-107">At hello command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="4f51d-108">Cette commande s’applique uniquement les correctifs logiciels tooregular.</span><span class="sxs-lookup"><span data-stu-id="4f51d-108">This command applies only tooregular hotfixes.</span></span> <span data-ttu-id="4f51d-109">Vous exécutez cette commande sur un seul contrôleur, mais les deux contrôleurs sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="4f51d-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="4f51d-110">Vous pouvez remarquer un basculement de contrôleur pendant le processus de mise à jour hello ; Toutefois, hello basculement affecteront pas la disponibilité du système ou l’opération.</span><span class="sxs-lookup"><span data-stu-id="4f51d-110">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="4f51d-111">Lorsque vous y êtes invité, fournissez hello chemin d’accès toohello dossier réseau partagé qui contient les fichiers de correctifs logiciels hello.</span><span class="sxs-lookup"><span data-stu-id="4f51d-111">When prompted, supply hello path toohello network shared folder that contains hello hotfix files.</span></span>
5. <span data-ttu-id="4f51d-112">Vous êtes invité à confirmer l’opération.</span><span class="sxs-lookup"><span data-stu-id="4f51d-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="4f51d-113">Type **Y** tooproceed avec l’installation du correctif logiciel hello.</span><span class="sxs-lookup"><span data-stu-id="4f51d-113">Type **Y** tooproceed with hello hotfix installation.</span></span>

