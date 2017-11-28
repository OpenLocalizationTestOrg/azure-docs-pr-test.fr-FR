
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, the following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through the new Azure portal
-->


1. <span data-ttu-id="c3393-101">Connectez-vous au [Portail Azure](https://portal.azure.com/) à l’adresse http://portal.azure.com/.</span><span class="sxs-lookup"><span data-stu-id="c3393-101">Log in to the [Azure portal](https://portal.azure.com/) at http://portal.azure.com/.</span></span>
2. <span data-ttu-id="c3393-102">Dans la bannière de gauche, cliquez sur **PARCOURIR TOUT**.</span><span class="sxs-lookup"><span data-stu-id="c3393-102">In the left banner, click **BROWSE ALL**.</span></span> <span data-ttu-id="c3393-103">Le panneau **Parcourir** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c3393-103">The **Browse** blade is displayed.</span></span>
3. <span data-ttu-id="c3393-104">Faites défiler l’écran, puis cliquez sur **Serveurs SQL**.</span><span class="sxs-lookup"><span data-stu-id="c3393-104">Scroll and click **SQL servers**.</span></span> <span data-ttu-id="c3393-105">Le panneau **Serveurs SQL** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c3393-105">The **SQL servers** blade is displayed.</span></span>
   
    ![Rechercher votre serveur Azure SQL Database sur le portail][b21-FindServerInPortal]
4. <span data-ttu-id="c3393-107">Pour plus de commodité, cliquez sur la commande de réduction sur le panneau **Parcourir** précédent.</span><span class="sxs-lookup"><span data-stu-id="c3393-107">For convenience, click the minimize control on the earlier **Browse** blade.</span></span>
5. <span data-ttu-id="c3393-108">Dans la zone de texte de filtre, tapez les premières lettres du nom de votre serveur.</span><span class="sxs-lookup"><span data-stu-id="c3393-108">In the filter text box, start typing the name of your server.</span></span> <span data-ttu-id="c3393-109">La ligne correspondante s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c3393-109">Your row is displayed.</span></span>
6. <span data-ttu-id="c3393-110">Cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="c3393-110">Click the row for your server.</span></span> <span data-ttu-id="c3393-111">Un panneau dédié à votre serveur s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c3393-111">A blade for your server is displayed.</span></span>
7. <span data-ttu-id="c3393-112">Dans ce panneau, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="c3393-112">On your server blade, click **Settings**.</span></span> <span data-ttu-id="c3393-113">Le panneau **Paramètres** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c3393-113">The **Settings** blade is displayed.</span></span>
8. <span data-ttu-id="c3393-114">Cliquez sur **Pare-feu**.</span><span class="sxs-lookup"><span data-stu-id="c3393-114">Click **Firewall**.</span></span> <span data-ttu-id="c3393-115">Le panneau **Paramètres du pare-feu** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c3393-115">The **Firewall Settings** blade is displayed.</span></span>
   
    ![Cliquer sur Paramètres, puis sur Pare-feu][b31-SettingsFirewallNavig]
9. <span data-ttu-id="c3393-117">Cliquez sur **Ajouter une adresse IP cliente**.</span><span class="sxs-lookup"><span data-stu-id="c3393-117">Click **Add Client IP**.</span></span> <span data-ttu-id="c3393-118">Dans la première zone de texte, tapez un nom pour votre nouvelle règle.</span><span class="sxs-lookup"><span data-stu-id="c3393-118">Type in a name for your new rule into the first text box.</span></span>
10. <span data-ttu-id="c3393-119">Tapez les valeurs d’adresse IP basse et haute de la plage que vous souhaitez autoriser.</span><span class="sxs-lookup"><span data-stu-id="c3393-119">Type in the low and high IP address values for the range you want to enable.</span></span>
    
    * <span data-ttu-id="c3393-120">Pour des raisons pratiques, vous pouvez terminer les valeurs basse et haute par **.0** et **.255**, respectivement.</span><span class="sxs-lookup"><span data-stu-id="c3393-120">It can be handy to have the low value end with **.0** and the high with **.255**.</span></span>
    
    ![Ajouter une plage d’adresses IP à autoriser][b41-AddRange]
11. <span data-ttu-id="c3393-122">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c3393-122">Click **Save**.</span></span>

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
