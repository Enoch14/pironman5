.. note::

    Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
    - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

    👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

.. _set_up_pironman5:

5. Einrichtung des Pironman 5
===================================

Vor der Konfiguration
--------------------------
Nach dem Einschalten sehen Sie nur die verschiedenen Power-LEDs leuchten, aber der OLED-Bildschirm (bei einem Anzeigeproblem ignorieren Sie es bitte, da es sich nach der Konfiguration löst), die RGB-LEDs und die RGB-Lüfter (die beiden Lüfter an den Seiten) funktionieren noch nicht, da sie noch nicht konfiguriert wurden.

Der Power-Button fungiert wie der Power-Button des Raspberry Pi 5 und funktioniert genauso.

**Herunterfahren**

    * Wenn Sie das Raspberry Pi **Bookworm Desktop**-System verwenden, können Sie den Power-Button zweimal schnell hintereinander drücken, um das Gerät herunterzufahren.
    * Wenn Sie das Raspberry Pi **Bookworm Lite**-System verwenden, drücken Sie den Power-Button einmal, um das Herunterfahren zu starten.
    * Um ein erzwungenes Herunterfahren durchzuführen, halten Sie den Power-Button gedrückt.

**Einschalten**

    * Wenn das Raspberry Pi Board heruntergefahren, aber noch mit Strom versorgt ist, drücken Sie einmal, um es aus dem Heruntergefahren-Zustand einzuschalten.

.. note::

    Wenn Sie ein System verwenden, das keinen Shutdown-Button unterstützt, können Sie ihn 5 Sekunden lang gedrückt halten, um ein erzwungenes Herunterfahren durchzuführen, und einmal drücken, um aus dem Heruntergefahren-Zustand einzuschalten.


Konfiguration des Herunterfahrens zur Deaktivierung der GPIO-Stromversorgung
-------------------------------------------------------------------------------------
Um zu verhindern, dass der OLED-Bildschirm und die RGB-Lüfter, die über den Raspberry Pi GPIO mit Strom versorgt werden, nach dem Herunterfahren aktiv bleiben, ist es wichtig, den Raspberry Pi so zu konfigurieren, dass die GPIO-Stromversorgung deaktiviert wird.

* Bearbeiten Sie die ``EEPROM``-Konfigurationsdatei manuell mit diesem Befehl:

  .. code-block:: shell

    sudo rpi-eeprom-config -e

* Ändern Sie die Einstellung ``POWER_OFF_ON_HALT`` in der Datei auf ``1``. Zum Beispiel:

  .. code-block:: shell

    BOOT_UART=1
    POWER_OFF_ON_HALT=1
    BOOT_ORDER=0xf41

* Press ``Ctrl + X``, ``Y`` and ``Enter`` to save the changes.


Herunterladen und Installieren des ``pironman5`` Moduls
-------------------------------------------------------------

.. note::

  Für Lite-Systeme installieren Sie zunächst Werkzeuge wie ``git``, ``python3``, ``pip3``, ``setuptools`` usw.
  
  .. code-block:: shell
  
    sudo apt-get update
    sudo apt-get install git -y
    sudo apt-get install python3 python3-pip python3-setuptools -y

Laden Sie den Code von GitHub herunter und installieren Sie das ``pironman5``-Modul.

.. code-block:: shell

  cd ~
  git clone https://github.com/sunfounder/pironman5.git
  cd ~/pironman5
  sudo python3 install.py

Nach erfolgreicher Installation ist ein Systemneustart erforderlich, um die Installation zu aktivieren. Befolgen Sie die Neustartaufforderung auf dem Bildschirm.

Nach dem Neustart startet der ``pironman5.service`` automatisch. Hier sind die Hauptkonfigurationen für |link_pironman5|:

  * Der OLED-Bildschirm zeigt CPU, RAM, Speichernutzung, CPU-Temperatur und die IP-Adresse des Raspberry Pi an.
  * Vier WS2812-RGB-LEDs leuchten in Blau im Atemmodus.

Sie können das ``systemctl``-Tool verwenden, um ``pironman5.service`` zu ``starten``, ``stoppen``, ``neu zu starten`` oder den ``Status`` zu überprüfen.

.. code-block:: shell

  sudo systemctl restart pironman5.service

* ``restart``: Verwenden Sie diesen Befehl, um Änderungen an den Einstellungen des Pironman 5 anzuwenden.
* ``start/stop``: Aktivieren oder deaktivieren Sie den ``pironman5.service``.
* ``status``: Überprüfen Sie den Betriebsstatus des ``pironman5``-Programms mit dem ``systemctl``-Tool.


View the Basic Configurations
-----------------------------------

The ``pironman5`` module offers basic configurations for Pironman, which you can review with the following command.

.. code-block:: shell

  pironman5 -c

The standard configurations appear as follows:

.. code-block:: 

  {
      "auto": {
          "rgb_color": "#0a1aff",
          "rgb_brightness": 50,
          "rgb_style": "breathing",
          "rgb_speed": 50,
          "rgb_enable": true,
          "rgb_led_count": 4,
          "temperature_unit": "C",
          "gpio_fan_mode": 2,
          "gpio_fan_pin": 6
      }
  }

Customize these configurations to fit your needs.

Use ``pironman5`` or ``pironman5 -h`` for instructions.

.. code-block::

  usage: pironman5-service [-h] [-c] [-rc [RGB_COLOR]] [-rb [RGB_BRIGHTNESS]]
                          [-rs [{solid,breathing,flow,flow_reverse,rainbow,rainbow_reverse,hue_cycle}]] [-rp [RGB_SPEED]]
                          [-re [RGB_ENABLE]] [-rl [RGB_LED_COUNT]] [-u [{C,F}]] [-gm [GPIO_FAN_MODE]] [-gp [GPIO_FAN_PIN]]
                          [{start,stop}]

  Pironman5

  positional arguments:
    {start,stop}          Command

  options:
    -h, --help            show this help message and exit
    -c, --config          Show config
    -rc [RGB_COLOR], --rgb-color [RGB_COLOR]
                          RGB color in hex format with or without # (e.g. #FF0000 or 00aabb)
    -rb [RGB_BRIGHTNESS], --rgb-brightness [RGB_BRIGHTNESS]
                          RGB brightness 0-100
    -rs [{solid,breathing,flow,flow_reverse,rainbow,rainbow_reverse,hue_cycle}], --rgb-style [{solid,breathing,flow,flow_reverse,rainbow,rainbow_reverse,hue_cycle}]
                          RGB style
    -rp [RGB_SPEED], --rgb-speed [RGB_SPEED]
                          RGB speed 0-100
    -re [RGB_ENABLE], --rgb-enable [RGB_ENABLE]
                          RGB enable True/False
    -rl [RGB_LED_COUNT], --rgb-led-count [RGB_LED_COUNT]
                          RGB LED count int
    -u [{C,F}], --temperature-unit [{C,F}]
                          Temperature unit
    -gm [GPIO_FAN_MODE], --gpio-fan-mode [GPIO_FAN_MODE]
                          GPIO fan mode, 0: Always On, 1: Performance, 2: Cool, 3: Balanced, 4: Quiet
    -gp [GPIO_FAN_PIN], --gpio-fan-pin [GPIO_FAN_PIN]
                          GPIO fan pin

.. note::

  Each time you modify the status of ``pironman5.service``, you need to use the following command to make the configuration changes take effect.

  .. code-block:: shell

    sudo systemctl restart pironman5.service

* Alternatively, inspect the program-generated log files.

  .. code-block:: shell

    cat /opt/pironman5/log

.. note::

<<<<<<< HEAD
  * Als nächstes können Sie die Komponenten des |link_pironman5| über das Dashboard anzeigen und steuern, siehe :ref:`view_control_dashboard`.
  * Wenn Sie Befehle verwenden möchten, siehe :ref:`view_control_commands`.
=======
  * Next, you can view and control the components of |link_pironman5| from dashboard, please refer to :ref:`view_control_dashboard`.
  * If you wish to use commands, please see :ref:`view_control_commands`.
>>>>>>> bee3badd7d521802059fd7f5755c629e0d35f0cc
