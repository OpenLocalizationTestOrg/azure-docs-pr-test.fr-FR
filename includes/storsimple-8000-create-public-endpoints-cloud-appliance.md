#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a>toocreate des points de terminaison publics sur l’équipement de cloud hello

1. Se connecter toohello portail Azure.
2. Accédez trop**virtuels**, puis sélectionnez et sur l’ordinateur virtuel hello qui est utilisé en tant que votre solution de cloud.
    
3. Vous devez toocreate un flux réseau sécurité (groupe) règle toocontrol hello du trafic vers et depuis votre machine virtuelle. Effectuer hello suivant les étapes toocreate une règle de groupe de sécurité réseau.
    1. Sélectionnez **Groupe de sécurité réseau**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. Cliquez sur le groupe de sécurité de réseau de valeur par défaut de hello est présenté.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. Sélectionnez **Règles de sécurité de trafic entrant**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. Cliquez sur **+ ajouter** toocreate une règle de sécurité de trafic entrant.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        Dans Panneau de règle hello ajouter sécurité de trafic entrant :

        1. Pourquoi **nom**, tapez ce qui suit hello nom pour le point de terminaison hello : WinRMHttps.
        
        2. Pourquoi **priorité**, sélectionnez un nombre inférieur à 1 000 (qui est la priorité de hello pour la règle par défaut de hello). Valeur hello est élevée, une priorité plus faible hello.

        3. Ensemble hello **Source** trop**tout**.

        4. Pourquoi **Service**, sélectionnez **WinRM**. Hello **protocole** est défini automatiquement trop**TCP** et hello **étendue du Port** est défini trop**5986**.

        5. Cliquez sur **OK** règle de hello toocreate.

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. L’étape finale consiste tooassociate groupe de sécurité de votre réseau avec un sous-réseau ou une interface réseau spécifique. Effectuer hello suivant les étapes tooassociate votre groupe de sécurité réseau avec un sous-réseau.
    1. Accédez trop**sous-réseaux**.
    2. Cliquez sur **+ Associer**.
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. Sélectionnez votre réseau virtuel, puis sous-réseau approprié de hello.
    4. Cliquez sur **OK** règle de hello toocreate.

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

Une fois que la règle de hello est créée, vous pouvez afficher son adresse IP virtuelle publique (VIP) de détails toodetermine hello. Enregistrez cette adresse.


