.. note::

    こんにちは、SunFounderのRaspberry Pi & Arduino & ESP32愛好家コミュニティへようこそ！Facebook上でRaspberry Pi、Arduino、ESP32についてもっと深く掘り下げ、他の愛好家と交流しましょう。

    **参加する理由は？**

    - **エキスパートサポート**：コミュニティやチームの助けを借りて、販売後の問題や技術的な課題を解決します。
    - **学び＆共有**：ヒントやチュートリアルを交換してスキルを向上させましょう。
    - **独占的なプレビュー**：新製品の発表や先行プレビューに早期アクセスしましょう。
    - **特別割引**：最新製品の独占割引をお楽しみください。
    - **祭りのプロモーションとギフト**：ギフトや祝日のプロモーションに参加しましょう。

    👉 私たちと一緒に探索し、創造する準備はできていますか？[|link_sf_facebook|]をクリックして今すぐ参加しましょう！


USB HDMIアダプター
==========================================

.. image:: img/hdmi_adapter.jpeg

このUSB HDMIアダプターボードは、Raspberry Pi 5専用に設計されています。主な機能は、USBおよびHDMI接続をUSBインターフェース側に位置合わせすることで、アクセス性とケーブル管理を向上させることです。

さらに、HDMIポートは標準のHDMI Type Aインターフェースに変換され、より広い互換性を提供します。

 **NVMe追加電源供給** 

このボードには、NVMe PIP電源供給用の5V電源ヘッダーがあります。拡張ヘッダーと組み合わせることで、NVMeの追加電源インターフェースに接続し、追加の電力を供給できます。

 **1220RTCバッテリーホルダー** 

1220RTCバッテリーホルダーが組み込まれており、RTCバッテリーの取り付けが簡単です。SH1.0 2P逆ケーブルを介して、Raspberry PiのRTCインターフェースに接続します。

このバッテリーホルダーは、CR1220およびML1220バッテリーの両方に対応しています。ML1220（リチウムマンガン電池）を使用する場合、Raspberry Piで直接充電を設定できます。なお、CR1220は充電不可です。

 **トリクル充電の有効化** 

.. warning::

  CR1220バッテリーを使用している場合、トリクル充電を有効にしないでください。バッテリーに修復不可能な損傷を与え、ボードを損傷する危険性があります。

デフォルトでは、バッテリーのトリクル充電機能は無効になっています。 ``sysfs`` ファイルには、現在のトリクル充電電圧と制限が示されています：

.. code-block:: shell

    pi@raspberrypi:~ $ cat /sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage
    0
    pi@raspberrypi:~ $ cat /sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage_max
    4400000
    pi@raspberrypi:~ $ cat /sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage_min
    1300000

トリクル充電を有効にするには、 ``/boot/firmware/config.txt`` に ``rtc_bbat_vchg`` を追加します：

  * ``/boot/firmware/config.txt`` を開きます。
  
    .. code-block:: shell
    
      sudo nano /boot/firmware/config.txt
      
  * ``/boot/firmware/config.txt`` に ``rtc_bbat_vchg`` を追加します。
  
    .. code-block:: shell
    
      dtparam=rtc_bbat_vchg=3000000
  
再起動後、システムは次のように表示されます：

.. code-block:: shell

    pi@raspberrypi:~ $ cat /sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage
    3000000
    pi@raspberrypi:~ $ cat /sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage_max
    4400000
    pi@raspberrypi:~ $ cat /sys/devices/platform/soc/soc:rpi_rtc/rtc/rtc0/charging_voltage_min
    1300000

これでバッテリーがトリクル充電されていることが確認できます。この機能を無効にするには、 ``config.txt`` から ``dtparam`` 行を削除するだけです。
