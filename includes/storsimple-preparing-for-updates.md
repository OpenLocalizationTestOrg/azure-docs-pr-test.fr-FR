<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="74dc4-101">Préparation des mises à jour</span><span class="sxs-lookup"><span data-stu-id="74dc4-101">Preparing for updates</span></span>
<span data-ttu-id="74dc4-102">Vous devez effectuer les étapes suivantes avant d’analyser et d’appliquer la mise à jour :</span><span class="sxs-lookup"><span data-stu-id="74dc4-102">You will need to perform the following steps before you scan and apply the update:</span></span>

1. <span data-ttu-id="74dc4-103">Prenez un instantané cloud des données de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="74dc4-103">Take a cloud snapshot of the device data.</span></span>
2. <span data-ttu-id="74dc4-104">Assurez-vous que les adresses IP fixes du contrôleur sont routables et peuvent se connecter à Internet.</span><span class="sxs-lookup"><span data-stu-id="74dc4-104">Ensure that your controller fixed IPs are routable and can connect to the Internet.</span></span> <span data-ttu-id="74dc4-105">Ces adresses IP fixes seront utilisées pour mettre en service les mises à jour sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="74dc4-105">These fixed IPs will be used to service updates to your device.</span></span> <span data-ttu-id="74dc4-106">Vous pouvez tester cette fonctionnalité en exécutant l’applet de commande suivante sur chaque contrôleur à partir de l’interface Windows PowerShell de l’appareil :</span><span class="sxs-lookup"><span data-stu-id="74dc4-106">You can test this by running the following cmdlet on each controller from the Windows PowerShell interface of the device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="74dc4-107">**Résultat de l’exemple pour Test-Connection lorsque des adresses IP fixes peuvent se connecter à Internet**</span><span class="sxs-lookup"><span data-stu-id="74dc4-107">**Sample output for Test-Connection when fixed IPs can connect to the Internet**</span></span>

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

<span data-ttu-id="74dc4-108">Une fois que vous avez terminé ces vérifications préalables manuelles, vous pouvez passer à l’analyse et à l’installation des mises à jour.</span><span class="sxs-lookup"><span data-stu-id="74dc4-108">After you have successfully completed these manual pre-checks, you can proceed to scan and install the updates.</span></span>

