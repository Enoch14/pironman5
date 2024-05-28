.. note::

    Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
    - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

    👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _set_up_rpi:

4. Einrichtung Ihres Raspberry Pi
=====================================

In diesem Kapitel lernen Sie, wie Sie sich beim Raspberry Pi anmelden. Wenn Sie einen Bildschirm haben, schließen Sie ihn an, um den Desktop des Raspberry Pi anzuzeigen.

Wenn Sie keinen Bildschirm haben, müssen Sie sich remote beim Raspberry Pi anmelden. Sie können auch den VNC Viewer verwenden, um auf den Desktop des Raspberry Pi zuzugreifen.

.. note::

    Wenn Sie bereits mit den Vorgängen des Raspberry Pi vertraut sind, können Sie dieses Kapitel überspringen.

Einrichtung mit einem Bildschirm
---------------------------------------

Ein Bildschirm vereinfacht die Arbeit mit Ihrem Raspberry Pi.

**Erforderliche Komponenten**

* |link_pironman5|
* Netzadapter
* MicroSD-Karte
* Bildschirm-Netzadapter
* HDMI-Kabel
* Bildschirm
* Maus
* Tastatur

Schritte:

#. Setzen Sie die MicroSD-Karte mit installiertem Raspberry Pi OS in den |link_pironman5| ein.

#. Schließen Sie Maus und Tastatur an den |link_pironman5| an.

#. Verwenden Sie das HDMI-Kabel, um den Bildschirm mit dem HDMI-Anschluss des |link_pironman5| zu verbinden. Stellen Sie sicher, dass der Bildschirm an eine Stromquelle angeschlossen und eingeschaltet ist.

#. Versorgen Sie den |link_pironman5| mit dem Netzadapter. Der Desktop des Raspberry Pi OS sollte nach einigen Sekunden auf dem Bildschirm erscheinen.

    .. image:: img/bookwarm.png
        :align: center

#. Jetzt können Sie das Terminal öffnen, um Befehle einzugeben.

Einrichtung ohne Bildschirm
------------------------------

Wenn Sie keinen Monitor haben, ist die Remote-Anmeldung eine praktikable Option.

Mit SSH können Sie auf die Bash-Shell des Raspberry Pi zugreifen, die die standardmäßige Linux-Shell ist. Bash bietet eine Kommandozeilenoberfläche zur Durchführung verschiedener Aufgaben.

Für diejenigen, die eine grafische Benutzeroberfläche (GUI) bevorzugen, ist die Remote-Desktop-Funktion eine bequeme Alternative zur Verwaltung von Dateien und Vorgängen.

**Erforderliche Komponenten**

* |link_pironman5|
* Netzadapter
* MicroSD-Karte

Schritte:

#. Setzen Sie die MicroSD-Karte mit installiertem Raspberry Pi OS in den |link_pironman5| ein.

#. Versorgen Sie den |link_pironman5| mit dem Netzadapter.

#. Für detaillierte Setup-Tutorials basierend auf Ihrem Betriebssystem, lesen Sie die folgenden Abschnitte:

.. toctree::

    remote_macosx
    remote_windows
    remote_linux
    remote_desktop
