### <a name="noconnection"></a>préfixes d’adresses toomodify réseau local passerelle IP - aucune connexion de passerelle

#### <a name="tooadd-additional-address-prefixes"></a>préfixes d’adresse supplémentaires tooadd :

1. Sur hello des ressources de passerelle de réseau Local, Bonjour **paramètres** , cliquez sur **Configuration**.
2. Ajouter un espace d’adressage IP hello Bonjour *ajouter la plage d’adresses supplémentaires* boîte.
3. Cliquez sur **enregistrer** toosave vos paramètres.

#### <a name="tooremove-address-prefixes"></a>préfixes d’adresse tooremove :

1. Sur hello des ressources de passerelle de réseau Local, Bonjour **paramètres** , cliquez sur **Configuration**.
2. Cliquez sur hello **'...'** sur la ligne hello contenant hello préfixe souhaité tooremove.
3. Cliquez sur **Supprimer**.
4. Cliquez sur **enregistrer** toosave vos paramètres.

### <a name="withconnection"></a>toomodify réseau local passerelle préfixes d’adresses IP - connexion de passerelle existante

Si vous disposez d’une connexion de passerelle et souhaitez tooadd ou supprimez des préfixes d’adresses IP hello contenues dans votre passerelle de réseau local, vous devez hello toodo comme suit, dans l’ordre. Cela entraînera une interruption de votre connexion VPN. Lorsque vous modifiez des préfixes d’adresses IP, vous n’avez pas besoin passerelle VPN de hello toodelete. Vous devez uniquement la connexion de hello tooremove.

#### <a name="1-remove-hello-connection"></a>1. Supprimer la connexion de hello.

1. Sur hello des ressources de passerelle de réseau Local, Bonjour **paramètres** , cliquez sur **connexions**.
2. Cliquez sur hello **...**  sur la ligne hello pour chaque connexion, puis cliquez sur **supprimer**.
3. Cliquez sur **enregistrer** toosave vos paramètres.

#### <a name="2-modify-hello-address-prefixes"></a>2. Modifier les préfixes d’adresse hello.

préfixes d’adresse supplémentaires tooadd :

1. Sur hello des ressources de passerelle de réseau Local, Bonjour **paramètres** , cliquez sur **Configuration**.
2. Ajouter un espace d’adressage IP hello.
3. Cliquez sur **enregistrer** toosave vos paramètres.

préfixes d’adresse tooremove :

1. Sur hello des ressources de passerelle de réseau Local, Bonjour **paramètres** , cliquez sur **Configuration**.
2. Cliquez sur hello **...**  sur la ligne hello contenant hello préfixe souhaité tooremove.
3. Cliquez sur **Supprimer**.
4. Cliquez sur **enregistrer** toosave vos paramètres.

#### <a name="3-recreate-hello-connection"></a>3. Recréez la connexion de hello.

1. Accédez toohello passerelle de réseau virtuel pour votre réseau virtuel. (Pas hello passerelle de réseau Local.)
2. Sur hello passerelle de réseau virtuel, Bonjour **paramètres** , cliquez sur **connexions**.
3. Cliquez sur hello **+ ajouter** tooopen hello **ajouter une connexion** panneau.
4. Recréez votre connexion.
5. Cliquez sur **OK** connexion de hello toocreate.
