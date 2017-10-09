<!--author=SharS last changed: 11/18/16-->

#### <a name="tooinstall-regular-updates-via-windows-powershell-for-storsimple"></a><span data-ttu-id="c9c32-101">mises à jour régulières de tooinstall via Windows PowerShell pour StorSimple</span><span class="sxs-lookup"><span data-stu-id="c9c32-101">tooinstall regular updates via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="c9c32-102">Ouvrez la console série du périphérique hello et sélectionnez l’option 1, **connecter avec un accès complet**.</span><span class="sxs-lookup"><span data-stu-id="c9c32-102">Open hello device serial console and select option 1, **Log in with full access**.</span></span> <span data-ttu-id="c9c32-103">Mot de passe type hello.</span><span class="sxs-lookup"><span data-stu-id="c9c32-103">Type hello password.</span></span> <span data-ttu-id="c9c32-104">mot de passe Hello *Password1*.</span><span class="sxs-lookup"><span data-stu-id="c9c32-104">hello default password is *Password1*.</span></span> 
2. <span data-ttu-id="c9c32-105">À l’invite de commandes hello, tapez :</span><span class="sxs-lookup"><span data-stu-id="c9c32-105">At hello command prompt, type:</span></span>
   
     `Get-HcsUpdateAvailability`
   
    <span data-ttu-id="c9c32-106">Vous êtes averti si des mises à jour sont disponibles et si les mises à jour hello sont sans interruption ou sans interruption de service.</span><span class="sxs-lookup"><span data-stu-id="c9c32-106">You will be notified if updates are available and whether hello updates are disruptive or non-disruptive.</span></span>
3. <span data-ttu-id="c9c32-107">À l’invite de commandes hello, tapez :</span><span class="sxs-lookup"><span data-stu-id="c9c32-107">At hello command prompt, type:</span></span>
   
     `Start-HcsUpdate`
   
    <span data-ttu-id="c9c32-108">processus de mise à jour Hello démarre.</span><span class="sxs-lookup"><span data-stu-id="c9c32-108">hello update process will start.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="c9c32-109">Cette commande s’applique uniquement les mises à jour tooregular.</span><span class="sxs-lookup"><span data-stu-id="c9c32-109">This command applies only tooregular updates.</span></span> <span data-ttu-id="c9c32-110">Vous exécutez cette commande sur un seul contrôleur, mais les deux contrôleurs sont mis à jour.</span><span class="sxs-lookup"><span data-stu-id="c9c32-110">You run this command on only one controller, but both controllers will be updated.</span></span> 
> * <span data-ttu-id="c9c32-111">Vous pouvez remarquer un basculement de contrôleur pendant le processus de mise à jour hello ; Toutefois, hello basculement affecteront pas la disponibilité du système ou l’opération.</span><span class="sxs-lookup"><span data-stu-id="c9c32-111">You may notice a controller failover during hello update process; however, hello failover will not affect system availability or operation.</span></span>
> 
> 

