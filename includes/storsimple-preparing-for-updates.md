<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="de28c-101">Préparation des mises à jour</span><span class="sxs-lookup"><span data-stu-id="de28c-101">Preparing for updates</span></span>
<span data-ttu-id="de28c-102">Vous devez hello tooperform comme suit avant d’analyser et appliquer la mise à jour hello :</span><span class="sxs-lookup"><span data-stu-id="de28c-102">You will need tooperform hello following steps before you scan and apply hello update:</span></span>

1. <span data-ttu-id="de28c-103">Prendre un instantané cloud de données de l’appareil hello.</span><span class="sxs-lookup"><span data-stu-id="de28c-103">Take a cloud snapshot of hello device data.</span></span>
2. <span data-ttu-id="de28c-104">Assurez-vous que votre contrôleur adresses IP fixe soient routable et peuvent se connecter toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="de28c-104">Ensure that your controller fixed IPs are routable and can connect toohello Internet.</span></span> <span data-ttu-id="de28c-105">Ces adresses IP fixes seront appareil de tooyour tooservice utilisé mises à jour.</span><span class="sxs-lookup"><span data-stu-id="de28c-105">These fixed IPs will be used tooservice updates tooyour device.</span></span> <span data-ttu-id="de28c-106">Vous pouvez le tester en exécutant hello suivant l’applet de commande sur chaque contrôleur à partir de l’interface Windows PowerShell de hello du périphérique de hello :</span><span class="sxs-lookup"><span data-stu-id="de28c-106">You can test this by running hello following cmdlet on each controller from hello Windows PowerShell interface of hello device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="de28c-107">**Exemple de sortie de Test-Connection lorsque les adresses IP fixes peuvent se connecter toohello Internet**</span><span class="sxs-lookup"><span data-stu-id="de28c-107">**Sample output for Test-Connection when fixed IPs can connect toohello Internet**</span></span>

        Controller0>Test-Connection -Source 10.126.173.91 -Destination bing.com

        Source      Destination     IPV4Address      IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200

        Controller0>Test-Connection -Source 10.126.173.91 -Destination  204.79.197.200

        Source      Destination       IPV4Address    IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200

<span data-ttu-id="de28c-108">Une fois que vous avez terminé ces vérifications préalables manuelles, vous pouvez continuer tooscan et installer des mises à jour hello.</span><span class="sxs-lookup"><span data-stu-id="de28c-108">After you have successfully completed these manual pre-checks, you can proceed tooscan and install hello updates.</span></span>

