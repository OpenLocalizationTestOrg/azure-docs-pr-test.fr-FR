<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a>Préparation des mises à jour
Vous devez hello tooperform comme suit avant d’analyser et appliquer la mise à jour hello :

1. Prendre un instantané cloud de données de l’appareil hello.
2. Assurez-vous que votre contrôleur adresses IP fixe soient routable et peuvent se connecter toohello Internet. Ces adresses IP fixes seront appareil de tooyour tooservice utilisé mises à jour. Vous pouvez le tester en exécutant hello suivant l’applet de commande sur chaque contrôleur à partir de l’interface Windows PowerShell de hello du périphérique de hello :
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    **Exemple de sortie de Test-Connection lorsque les adresses IP fixes peuvent se connecter toohello Internet**

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

Une fois que vous avez terminé ces vérifications préalables manuelles, vous pouvez continuer tooscan et installer des mises à jour hello.

