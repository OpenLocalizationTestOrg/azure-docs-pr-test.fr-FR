
#### <a name="tooconfigure-remote-management-on-cloud-appliance"></a>tooconfigure de gestion à distance sur l’équipement de cloud

1. Dans le service StorSimple Device Manager, cliquez sur **Appareils**. Sélectionnez et cliquez sur votre matériel de cloud à partir de la liste de hello de périphériques connectés toohello service.
    ![StorSimple - sélectionner une appliance cloud](./media/storsimple-8000-configure-remote-management-http-device/sca-remote-manage1.png)

2. Accédez trop**Paramètres > sécurité** tooopen hello **paramètres de sécurité** panneau.

     ![Paramètres de sécurité StorSimple](./media/storsimple-8000-configure-remote-management-http-device/sca-remote-manage2.png)

3. Accédez toohello **gestion à distance** section. Cochez la case **Gestion à distance**.
     ![StorSimple - Gestion à distance](./media/storsimple-8000-configure-remote-management-http-device/sca-remote-manage3.png)

4. Bonjour **gestion à distance** panneau :

    1. Vérifiez que la case **Activer l’administration à distance** est cochée.
    2. valeur par défaut Hello est tooconnect via le protocole HTTPS. Vous pouvez choisir tooconnect à l’aide de HTTP. Une connexion via HTTP est acceptable uniquement sur des réseaux approuvés. Vérifiez que HTTP est activé.
    3. Dans la barre de commandes hello haut hello du panneau, cliquez sur **... Plus** puis cliquez sur **télécharger le certificat** toodownload un certificat de gestion à distance. Vous pouvez spécifier un emplacement dans le toosave de ce fichier. Ce certificat doit être installé sur l’ordinateur client ou l’hôte de hello utiliser tooconnect toohello cloud application.

        ![Panneau de gestion à distance](./media/storsimple-8000-configure-remote-management-http-device/sca-remote-manage4.png)
5. Cliquez sur **enregistrer** et lorsque vous y êtes invité, confirmez les modifications hello.
