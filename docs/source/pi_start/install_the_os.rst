.. note::

    こんにちは、SunFounderのRaspberry Pi & Arduino & ESP32愛好家コミュニティへようこそ！Facebook上でRaspberry Pi、Arduino、ESP32についてもっと深く掘り下げ、他の愛好家と交流しましょう。

    **参加する理由は？**

    - **エキスパートサポート**：コミュニティやチームの助けを借りて、販売後の問題や技術的な課題を解決します。
    - **学び＆共有**：ヒントやチュートリアルを交換してスキルを向上させましょう。
    - **独占的なプレビュー**：新製品の発表や先行プレビューに早期アクセスしましょう。
    - **特別割引**：最新製品の独占割引をお楽しみください。
    - **祭りのプロモーションとギフト**：ギフトや祝日のプロモーションに参加しましょう。

    👉 私たちと一緒に探索し、創造する準備はできていますか？[|link_sf_facebook|]をクリックして今すぐ参加しましょう！

3. オペレーティングシステムのインストール
==========================================

この章では、オペレーティングシステムのインストール方法を学びます。

.. note::

    Raspberry Pi 5をサポートするOSをインストールする必要があります。最新のRaspberry Pi Imagerツールを使用してシステムをインストールしてください。現在テスト済みのシステムは以下の通りです：

    * **Raspberry Pi OS (bookworm 64 desktop / lite)**: 完全に互換性あり
    * **Ubuntu Desktop 23.10**: SPIが動作せず、LEDが点灯しない
    * **Kali**: I2Cが動作せず、OLEDスクリーンが点灯しない
    * **Home Assistant**: I2CとSPIを有効にできない

**1. OSをMicro SDカードにインストール** 

Micro SDカードを使用する場合は、以下のチュートリアルに従ってシステムをMicro SDカードにインストールできます。

.. toctree::
    :maxdepth: 1

    install_to_sd

**2. OSをNVMe SSDにインストール** 

NVMe SSDを使用し、システムインストールのためにNVMe SSDをコンピュータに接続するアダプタがある場合は、以下のチュートリアルを使用して迅速にインストールできます。

.. toctree::
    :maxdepth: 1

    install_to_nvme

**3. Micro SDカードからNVMe SSDへOSをコピー** 

NVMe SSDをお持ちで、NVMeをコンピュータに接続するアダプタがない場合は、まずMicro SDカードにシステムをインストールします。 |link_pironman5| が正常に起動した後、Micro SDカードからNVMe SSDにシステムをコピーできます。詳細な手順は以下の通りです：

以下の手順に従ってください：

1. Micro SDカードにシステムをインストールします。

* :ref:`install_os_sd`

2. Raspberry Piを起動してログインします。

* :ref:`set_up_rpi`

3. NVMe SSDからのブートを設定し、Micro SDカードからNVMe SSDにシステムをコピーするか、Raspberry Piシステム内のImagerを使用してシステムを直接NVMe SSDにインストールします。

* :ref:`boot_from_ssd`
