
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. <span data-ttu-id="42051-101">Connectez-vous à toohello [portail Azure](https://portal.azure.com/) à http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="42051-101">Log in toohello [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="42051-102">Dans la bannière de gauche hello, cliquez sur **parcourir tous les**.</span><span class="sxs-lookup"><span data-stu-id="42051-102">In hello left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="42051-103">Hello **Parcourir** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="42051-103">hello **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="42051-104">Faites défiler l’écran, puis cliquez sur **Serveurs SQL**.</span><span class="sxs-lookup"><span data-stu-id="42051-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="42051-105">Hello **serveurs SQL** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="42051-105">hello **SQL servers** blade is displayed.</span></span>
   
    ![Recherchez votre serveur de base de données SQL Azure dans le portail de hello][b21-FindServerInPortal]
4. <span data-ttu-id="42051-107">Pour plus de commodité, cliquez sur hello réduire contrôle sur hello précédemment **Parcourir** panneau.</span><span class="sxs-lookup"><span data-stu-id="42051-107">For convenience, click hello minimize control on hello earlier **Browse** blade.</span></span>
5. <span data-ttu-id="42051-108">Dans la zone de texte de filtre hello, commencez à taper nom de hello de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="42051-108">In hello filter text box, start typing hello name of your server.</span></span> <span data-ttu-id="42051-109">La ligne correspondante s’affiche.</span><span class="sxs-lookup"><span data-stu-id="42051-109">Your row is displayed.</span></span>
6. <span data-ttu-id="42051-110">Cliquez sur ligne hello pour votre serveur.</span><span class="sxs-lookup"><span data-stu-id="42051-110">Click hello row for your server.</span></span> <span data-ttu-id="42051-111">Un panneau dédié à votre serveur s’affiche.</span><span class="sxs-lookup"><span data-stu-id="42051-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="42051-112">Dans ce panneau, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="42051-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="42051-113">Hello **paramètres** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="42051-113">hello **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="42051-114">Cliquez sur **Pare-feu**.</span><span class="sxs-lookup"><span data-stu-id="42051-114">Click **Firewall**.</span></span> <span data-ttu-id="42051-115">Hello **les paramètres de pare-feu** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="42051-115">hello **Firewall Settings** blade is displayed.</span></span>
   
    ![Cliquer sur Paramètres, puis sur Pare-feu][b31-SettingsFirewallNavig]
9. <span data-ttu-id="42051-117">Cliquez sur **Ajouter une adresse IP cliente**.</span><span class="sxs-lookup"><span data-stu-id="42051-117">Click **Add Client IP**.</span></span> <span data-ttu-id="42051-118">Tapez un nom pour votre nouvelle règle dans la première zone de texte hello.</span><span class="sxs-lookup"><span data-stu-id="42051-118">Type in a name for your new rule into hello first text box.</span></span>
10. <span data-ttu-id="42051-119">Type Bonjour haute et basse de valeurs de plage hello d’adresses IP tooenable.</span><span class="sxs-lookup"><span data-stu-id="42051-119">Type in hello low and high IP address values for hello range you want tooenable.</span></span>
    
    * <span data-ttu-id="42051-120">Il peut être pratique toohave hello faible valeur de fin avec **.0** et hello élevé avec **.255**.</span><span class="sxs-lookup"><span data-stu-id="42051-120">It can be handy toohave hello low value end with **.0** and hello high with **.255**.</span></span>
    
    ![Ajouter un tooallow de plage d’adresses IP][b41-AddRange]
11. <span data-ttu-id="42051-122">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="42051-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
