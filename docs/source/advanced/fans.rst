.. note::

    Hallo und willkommen in der SunFounder Raspberry Pi & Arduino & ESP32 Enthusiasten-Gemeinschaft auf Facebook! Tauchen Sie tiefer ein in die Welt von Raspberry Pi, Arduino und ESP32 mit anderen Enthusiasten.

    **Warum beitreten?**

    - **Expertenunterstützung**: Lösen Sie Nachverkaufsprobleme und technische Herausforderungen mit Hilfe unserer Gemeinschaft und unseres Teams.
    - **Lernen & Teilen**: Tauschen Sie Tipps und Anleitungen aus, um Ihre Fähigkeiten zu verbessern.
    - **Exklusive Vorschauen**: Erhalten Sie frühzeitigen Zugang zu neuen Produktankündigungen und exklusiven Einblicken.
    - **Spezialrabatte**: Genießen Sie exklusive Rabatte auf unsere neuesten Produkte.
    - **Festliche Aktionen und Gewinnspiele**: Nehmen Sie an Gewinnspielen und Feiertagsaktionen teil.

    👉 Sind Sie bereit, mit uns zu erkunden und zu erschaffen? Klicken Sie auf [|link_sf_facebook|] und treten Sie heute bei!

Lüfter
============

PWM-Lüfter
---------------

Der PWM-Lüfter des |link_pironman5| wird vom Raspberry Pi System gesteuert.

Hinsichtlich der Kühlungslösungen für den Raspberry Pi 5, insbesondere unter hoher Last, integriert das Design des |link_pironman5| ein intelligentes Kühlsystem. Es umfasst einen primären PWM-Lüfter und zwei zusätzliche RGB-Lüfter. Die Kühlstrategie ist eng mit dem Wärmemanagementsystem des Raspberry Pi 5 verbunden.

Der Betrieb des PWM-Lüfters basiert auf der Temperatur des Raspberry Pi 5:

* Unter 50°C bleibt der PWM-Lüfter aus (0% Geschwindigkeit).
* Bei 50°C startet der Lüfter mit niedriger Geschwindigkeit (30% Geschwindigkeit).
* Bei 60°C erhöht sich die Lüftergeschwindigkeit auf mittlere Stufe (50% Geschwindigkeit).
* Bei 67,5°C läuft der Lüfter mit hoher Geschwindigkeit (70% Geschwindigkeit).
* Ab 75°C und darüber hinaus arbeitet der Lüfter mit voller Geschwindigkeit (100% Geschwindigkeit).

Diese Temperatur-Geschwindigkeits-Beziehung gilt auch beim Abkühlen, wobei eine Hysterese von 5°C besteht. Die Lüftergeschwindigkeit wird reduziert, wenn die Temperatur um 5°C unter die jeweiligen Schwellenwerte fällt.

* Befehle zur Überwachung des PWM-Lüfters. Um den Status des PWM-Lüfters zu überprüfen:

  .. code-block:: shell
  
    cat /sys/class/thermal/cooling_device0/cur_state

* Um die Geschwindigkeit des PWM-Lüfters anzuzeigen:

  .. code-block:: shell

    cat /sys/devices/platform/cooling_fan/hwmon/*/fan1_input

Im |link_pironman5| ist der PWM-Lüfter ein kritisches Element zur Aufrechterhaltung optimaler Betriebstemperaturen, insbesondere bei intensiven Aufgaben, und gewährleistet, dass der Raspberry Pi 5 effizient und zuverlässig läuft.

RGB-Lüfter
-------------------

.. image:: img/size_fan.png

* **Abmessungen**: 40*40*10MM
* **Gewicht**: 13,5±5g/Stk.
* **Lebensdauer**: 40.000 Stunden (Raumtemperatur 25°C)
* **Maximaler Luftstrom**: 2,46CFM
* **Maximaler Luftdruck**: 0,62mm-H2O
* **Lautstärke**: 22,31dBA
* **Nennleistung**: 5V/0.1A
* **Nenn-Geschwindigkeit**: 3500±10%RPM
* **Betriebstemperatur**: -10℃~+70℃
* **Lagertemperatur**: -30℃~+85℃

