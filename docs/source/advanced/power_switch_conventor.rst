.. note::

    Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
    - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

    👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

Power Switch Konverter
==============================

Dies ist ein Modul, das den Netzschalter des Raspberry Pi 5 nach außen erweitert.

.. image:: img/power_switch_conventor.jpeg

**Hinzufügen des Netzschalters**

* Der Raspberry Pi 5 verfügt über einen **J2**-Jumper, der sich zwischen dem RTC-Batterieanschluss und dem Rand der Platine befindet. Dieser Anschluss ermöglicht die Hinzufügung eines benutzerdefinierten Netzschalters zum Raspberry Pi 5, indem ein normalerweise offener (NO) Taster über die beiden Pads verbunden wird. Durch kurzes Drücken dieses Schalters wird die Funktionalität des onboard Netzschalters nachgeahmt.

    .. image:: img/pi5_j2.jpg

* Auf dem |link_pironman5| gibt es einen **Power Switch Converter**, der den **J2**-Jumper zu einem externen Netzschalter mit zwei Pogo-Pins erweitert.

    .. image:: img/power_switch_convertor.png

* Nun kann der Raspberry Pi 5 mit dem Netzschalter ein- und ausgeschaltet werden.

    .. image:: img/pironman_button.JPG

**Power Cycling**

Beim erstmaligen Einschalten des Raspberry Pi 5 wird er automatisch eingeschaltet und startet das Betriebssystem, ohne dass der Netzschalter gedrückt werden muss.

Wenn der Raspberry Pi Desktop ausgeführt wird, führt ein kurzes Drücken des Netzschalters zu einem ordnungsgemäßen Herunterfahren. Ein Menü wird angezeigt, das Optionen zum Herunterfahren, Neustarten oder Abmelden bietet. Durch Auswählen einer Option oder erneutes Drücken des Netzschalters wird ein ordnungsgemäßes Herunterfahren eingeleitet.

.. image:: img/button_shutdown.png

**Herunterfahren**

    * Wenn Sie das Raspberry Pi **Bookworm Desktop**-System ausführen, können Sie den Netzschalter zweimal schnell hintereinander drücken, um herunterzufahren.
    * Wenn Sie das Raspberry Pi **Bookworm Lite**-System ohne Desktop ausführen, drücken Sie den Netzschalter einmal, um ein Herunterfahren zu initiieren.
    * Um ein hartes Herunterfahren zu erzwingen, halten Sie den Netzschalter gedrückt.

**Einschalten**

    * Wenn das Raspberry Pi-Board heruntergefahren, aber noch mit Strom versorgt ist, drücken Sie einmal, um es aus dem Heruntergefahren-Zustand einzuschalten.

.. note::

    Wenn Sie ein System verwenden, das keinen Herunterfahrknopf unterstützt, können Sie den Knopf 5 Sekunden lang gedrückt halten, um ein hartes Herunterfahren zu erzwingen, und einmal drücken, um es aus dem Heruntergefahren-Zustand einzuschalten.
