.. note::

    Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
    - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

    👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

Installation des Betriebssystems auf einer NVMe-SSD
==========================================================

**Erforderliche Komponenten**

* Ein Personal Computer
* Eine NVMe-SSD
* Ein NVMe-zu-USB-Adapter
* MicroSD-Karte und Kartenleser

1. Raspberry Pi Imager installieren
--------------------------------------

#. Besuchen Sie die Raspberry Pi Software-Download-Seite unter `Raspberry Pi Imager <https://www.raspberrypi.org/software/>`_. Wählen Sie die Imager-Version aus, die mit Ihrem Betriebssystem kompatibel ist. Laden Sie die Datei herunter und öffnen Sie sie, um die Installation zu starten.

    .. image:: img/os_install_imager.png
        :align: center

#. Je nach Betriebssystem kann während der Installation eine Sicherheitsaufforderung erscheinen. Beispielsweise zeigt Windows möglicherweise eine Warnmeldung an. In solchen Fällen wählen Sie **Weitere Informationen** und dann **Trotzdem ausführen**. Folgen Sie den Anweisungen auf dem Bildschirm, um die Installation des Raspberry Pi Imager abzuschließen.

    .. image:: img/os_info.png
        :align: center

#. Starten Sie die Raspberry Pi Imager-Anwendung, indem Sie auf das Symbol klicken oder ``rpi-imager`` in Ihrem Terminal eingeben.

    .. image:: img/os_open_imager.png
        :align: center

2. Bootloader aktualisieren
------------------------------

Zuerst müssen Sie den Bootloader des Raspberry Pi 5 aktualisieren, um von NVMe zu booten, bevor USB und dann die SD-Karte versucht werden.

.. note::

    In diesem Schritt wird empfohlen, eine Ersatz-MicroSD-Karte zu verwenden. Schreiben Sie zuerst den Bootloader auf diese MicroSD-Karte und stecken Sie sie dann sofort in den Raspberry Pi, um das Booten von einem NVMe-Gerät zu ermöglichen.
    
    Alternativ können Sie den Bootloader zuerst direkt auf Ihr NVMe-Gerät schreiben und es dann in den Raspberry Pi einstecken, um dessen Bootmethode zu ändern. Danach schließen Sie die NVMe-SSD an einen Computer an, um das Betriebssystem zu installieren, und sobald die Installation abgeschlossen ist, setzen Sie sie wieder in den Raspberry Pi ein.

#. Setzen Sie Ihre Ersatz-MicroSD-Karte oder NVMe-SSD mit einem Kartenleser in Ihren Computer oder Laptop ein.

#. Wählen Sie im Imager **Raspberry Pi Gerät** und dann das Modell **Raspberry Pi 5** aus der Dropdown-Liste aus.

    .. image:: img/os_choose_device_pi5.png
        :align: center

#. Im Tab **Betriebssystem** scrollen Sie nach unten und wählen **Verschiedene Dienstprogramme**.

    .. image:: img/nvme_misc.png
        :align: center

#. Wählen Sie **Bootloader (Pi 5 Familie)**.

    .. image:: img/nvme_bootloader.png
        :align: center

#. Wählen Sie **NVMe/USB Boot** aus, um den Raspberry Pi 5 so zu konfigurieren, dass er von NVMe bootet, bevor USB und dann die SD-Karte versucht werden.

    .. image:: img/nvme_nvme_boot.png
        :align: center

#. Wählen Sie in der **Speicher**-Option Ihre eingesetzte NVMe-SSD aus.

    .. note::

        Stellen Sie sicher, dass Sie das richtige Speichermedium auswählen. Um Verwirrung zu vermeiden, trennen Sie alle zusätzlichen Speichermedien, wenn mehrere angeschlossen sind.

    .. image:: img/nvme_ssd_storage.png
        :align: center

#. Jetzt können Sie auf **Weiter** klicken. Wenn das Speichermedium vorhandene Daten enthält, sichern Sie diese, um Datenverlust zu vermeiden. Fahren Sie fort, indem Sie **Ja** klicken, wenn keine Sicherung erforderlich ist.

    .. image:: img/nvme_erase.png
        :align: center

#. Bald erhalten Sie die Meldung, dass **NVMe/USB Boot** auf Ihr Speichermedium geschrieben wurde.

    .. image:: img/nvme_boot_finish.png
        :align: center

#. Jetzt können Sie Ihre MicroSD-Karte oder NVMe-SSD in den |link_pironman5| einsetzen. Nachdem Sie den |link_pironman5| mit einem Typ-C-Adapter eingeschaltet haben, wird der Bootloader von der MicroSD-Karte oder NVMe-SSD in das EEPROM des Raspberry Pi geschrieben.

.. note::

    Danach wird der Raspberry Pi von NVMe booten, bevor USB und dann die SD-Karte versucht werden.
    
    Schalten Sie den |link_pironman5| aus und entfernen Sie die MicroSD-Karte oder NVMe-SSD.

3. Betriebssystem auf NVMe-SSD installieren
-----------------------------------------------------

Jetzt können Sie das Betriebssystem auf Ihrer NVMe-SSD installieren.

#. Wählen Sie im Imager **Raspberry Pi Gerät** und dann das Modell **Raspberry Pi 5** aus der Dropdown-Liste aus.

    .. image:: img/os_choose_device_pi5.png
        :align: center

#. Wählen Sie **Betriebssystem** und entscheiden Sie sich für die empfohlene Betriebssystemversion.

    .. image:: img/os_choose_os.png
        :align: center

#. Wählen Sie in der **Speicher**-Option Ihre eingesetzte NVMe-SSD aus.

    .. note::

        Stellen Sie sicher, dass Sie das richtige Speichermedium auswählen. Um Verwirrung zu vermeiden, trennen Sie alle zusätzlichen Speichermedien, wenn mehrere angeschlossen sind.

    .. image:: img/nvme_ssd_storage.png
        :align: center

#. Klicken Sie auf **Weiter** und dann auf **Einstellungen bearbeiten**, um Ihre Betriebssystemeinstellungen anzupassen.

    .. note::

        Wenn Sie einen Monitor für Ihren Raspberry Pi haben, können Sie die nächsten Schritte überspringen und auf 'Ja' klicken, um die Installation zu starten. Passen Sie andere Einstellungen später am Monitor an.

    .. image:: img/os_enter_setting.png
        :align: center

#. Definieren Sie einen **Hostname** für Ihren Raspberry Pi.

    .. note::

        Der Hostname ist der Netzwerkidentifikator Ihres Raspberry Pi. Sie können auf Ihren Pi über ``<hostname>.local`` oder ``<hostname>.lan`` zugreifen.

    .. image:: img/os_set_hostname.png
        :align: center

#. Erstellen Sie einen **Benutzernamen** und ein **Passwort** für das Administratorkonto des Raspberry Pi.

    .. note::

        Die Einrichtung eines eindeutigen Benutzernamens und Passworts ist wichtig, um Ihren Raspberry Pi zu sichern, der kein Standardpasswort hat.

    .. image:: img/os_set_username.png
        :align: center

#. Konfigurieren Sie das drahtlose LAN, indem Sie die **SSID** und das **Passwort** Ihres Netzwerks angeben.

    .. note::

        Stellen Sie das ``Wireless LAN country`` auf den zweistelligen `ISO/IEC alpha2 code <https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements>`_ ein, der Ihrem Standort entspricht.

    .. image:: img/os_set_wifi.png
        :align: center

#. Um remote auf Ihren Raspberry Pi zuzugreifen, **aktivieren Sie SSH** im Tab **Dienste**.

    * Für **Passwort-Authentifizierung** verwenden Sie den Benutzernamen und das Passwort aus dem Tab **Allgemein**.
    * Für die Authentifizierung mit öffentlichem Schlüssel wählen Sie "Nur öffentliche Schlüssel-Authentifizierung zulassen". Wenn Sie einen RSA-Schlüssel haben, wird dieser verwendet. Wenn nicht, klicken Sie auf "SSH-keygen ausführen", um ein neues Schlüsselpaar zu generieren.

    .. image:: img/os_enable_ssh.png
        :align: center

#. Das Menü **Optionen** ermöglicht die Konfiguration des Verhaltens des Imagers während des Schreibens, einschließlich Abspielen von Sounds bei Fertigstellung, Auswerfen von Medien bei Fertigstellung und Aktivierung der Telemetrie.

    .. image:: img/os_options.png
        :align: center

#. Wenn Sie mit der Eingabe der Betriebssystemanpassungseinstellungen fertig sind, klicken Sie auf **Speichern**, um Ihre Anpassungen zu speichern. Klicken Sie dann auf **Ja**, um sie beim Schreiben des Images anzuwenden.

    .. image:: img/os_click_yes.png
        :align: center

#. Wenn die NVMe-SSD vorhandene Daten enthält, stellen Sie sicher, dass Sie sie sichern, um Datenverlust zu vermeiden. Fahren Sie fort, indem Sie auf **Ja** klicken, wenn keine Sicherung erforderlich ist.

    .. image:: img/nvme_erase.png
        :align: center

#. Wenn Sie das Popup "Schreiben erfolgreich" sehen, wurde Ihr Image vollständig geschrieben und verifiziert. Sie sind nun bereit, einen Raspberry Pi von der NVMe-SSD zu booten!

    .. image:: img/nvme_install_finish.png
        :align: center

#. Setzen Sie nun die NVMe-SSD in die NVMe PiP-Platine des |link_pironman5| ein.

    .. image:: img/nvme_assemble.png
        :width: 500
        :align: center
