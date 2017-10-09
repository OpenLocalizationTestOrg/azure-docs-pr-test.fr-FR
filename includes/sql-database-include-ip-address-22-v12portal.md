
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. Connectez-vous à toohello [portail Azure](https://portal.azure.com/) à http://portal.azure.com/.
2. Dans la bannière de gauche hello, cliquez sur **parcourir tous les**. Hello **Parcourir** panneau s’affiche.
3. Faites défiler l’écran, puis cliquez sur **Serveurs SQL**. Hello **serveurs SQL** panneau s’affiche.
   
    ![Recherchez votre serveur de base de données SQL Azure dans le portail de hello][b21-FindServerInPortal]
4. Pour plus de commodité, cliquez sur hello réduire contrôle sur hello précédemment **Parcourir** panneau.
5. Dans la zone de texte de filtre hello, commencez à taper nom de hello de votre serveur. La ligne correspondante s’affiche.
6. Cliquez sur ligne hello pour votre serveur. Un panneau dédié à votre serveur s’affiche.
7. Dans ce panneau, cliquez sur **Paramètres**. Hello **paramètres** panneau s’affiche.
8. Cliquez sur **Pare-feu**. Hello **les paramètres de pare-feu** panneau s’affiche.
   
    ![Cliquer sur Paramètres, puis sur Pare-feu][b31-SettingsFirewallNavig]
9. Cliquez sur **Ajouter une adresse IP cliente**. Tapez un nom pour votre nouvelle règle dans la première zone de texte hello.
10. Type Bonjour haute et basse de valeurs de plage hello d’adresses IP tooenable.
    
    * Il peut être pratique toohave hello faible valeur de fin avec **.0** et hello élevé avec **.255**.
    
    ![Ajouter un tooallow de plage d’adresses IP][b41-AddRange]
11. Cliquez sur **Enregistrer**.

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
