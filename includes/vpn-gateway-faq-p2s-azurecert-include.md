[!INCLUDE [P2S FAQ All](vpn-gateway-faq-p2s-all-include.md)]

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>Puis-je utiliser ma propre AC racine PKI interne pour une connectivité point à site ?

Oui. Auparavant, seuls les certificats racines auto-signés pouvaient être utilisés. Vous pouvez toujours charger 20 certificats racine.

### <a name="what-tools-can-i-use-to-create-certificates"></a>Quels outils puis-je utiliser pour créer des certificats ?

Vous pouvez utiliser votre solution de PKI d’entreprise (votre PKI interne), Azure PowerShell, MakeCert et OpenSSL.

### <a name="certsettings"></a>Y a-t-il des instructions pour les paramètres de certificat ?

* **PKI interne/Solution PKI d’entreprise :** reportez-vous aux étapes de [génération des certificats](../articles/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal.md#generatecert).

* **Azure PowerShell :** consultez l’article [Azure PowerShell](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site.md) pour connaître la procédure.

* **MakeCert :** consultez l’article [MakeCert](../articles/vpn-gateway/vpn-gateway-certificates-point-to-site-makecert.md) pour connaître la procédure.

* **OpenSSL :** 

    * Lors de l’exportation de certificats, veillez à convertir le certificat racine en Base64.

    * Pour le certificat client :

      * Lorsque vous créez la clé privée, spécifiez la longueur 4096.
      * Lors de la création du certificat, pour le paramètre *-extensions*, spécifiez *usr_cert*.