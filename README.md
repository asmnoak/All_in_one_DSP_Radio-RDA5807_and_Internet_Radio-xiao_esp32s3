<p><H3> All-in-one DSP Radio(RDA5807) and Internet Radio</H3></p>
<p>
FM DSPラジオとインターネットラジオを合体したセットを製作したので紹介する。<br>
DSPラジオにはRDA5807FPを利用した（<a href="https://www.aitendo.com/product/4797">データシートの参照リンクあり</a>）。<br>
インターネットラジオにはDACとしてPCM5102を利用している。<br>
両者を合体し、<a href="https://www.switch-science.com/products/8968">Seeed Studio XIAO ESP32S3</a>で制御する。<br>
操作には、Webブラウザを使用する。<br>開発はArduino IDE 2.1で行った。<br>
使用したRDA5807用のライブラリは、<a href="https://github.com/pu2clr/RDA5807">こちら（pu2clr at GitHub）</a>にある。<br>
なお、Arduino IDEのライブラリ管理からもインストール可能である。<br>
I2SのライブラリaudioI2Sは、<a href="https://github.com/schreibfaul1/ESP32-audioI2S  ">こちら（GitHub）</a>(ただし、バージョンは3.0.12。このフォルダの”src.zip”)を利用している。
</p>
<p><strong>機能</strong><br>
 ・FMラジオとインターネットラジオを切替え可能。出力切替えには　アナログスイッチADG884 を利用している。<br>
 ・週間スケジュールを設定できる。曜日ごとに、開始時間、長さ（分）、ラジオ局又はインターネットラジオ局の番号、音量、終了後ON/OFFを設定する。<br>
 ・ラジオ局とインターネットラジオ局の区別は番号で行う。50以上をインターネットラジオ局と判断し、50を引いてインターネットラジオ局の番号とする。<br>
 ・週間スケジュールの設定は、PC、スマホ等のブラウザからXIAO ESP32S3にアクセスして行う。<br>
 ・同様に、ラジオ局又はインターネットラジオ局の選局、音量の変更、ラジオのON/OFFは、ブラウザから行うことができる。<br>
 ・週間スケジュールの設定により、目覚まし機能、スリープ機能が可能である。<br>
 ・OLED表示装置に、日付、曜日、時刻、音量、ラジオのON/OFF、受信周波数、インターネットラジオ局の情報を表示する。<br>
 ・XIAO ESP32S3の特定のピンにタクトスイッチを接続すれば、選局、音量調節、スリープが可能である。<br>
 ・受信周波数の範囲は、76－108MHzで、ワイドFM対応である。<br>
 ・出力はオーディオジャック経由で小口径のスピーカー（ステレオ）を接続する。<br>
</p>
<p><strong>H/W構成</strong><br>
 ・Seeed Studio XIAO ESP32S3 - コントローラ<br>
 ・I2C接続&nbsp; RDA5807FP<br>
 ・I2S接続&nbsp; PCM5102　(UDA1334でも可)<br>
 ・I2C接続&nbsp; SSD1306 64x32 OLED表示装置<br>
 ・出力切替え&nbsp; ADG884 アナログスイッチ<br>
 ・Xtal発振器（32768Hz）、コンデンサ、抵抗類、オーディオジャック、配線類<br>
</p>
<p>
<strong>回路図</strong><br>
<img src="./xiao_esp32s3_i_d_mini_sch_3.png" width="860" height="560"><br>
</p>
<p><strong>接続</strong><br>
各コンポーネントの接続は回路図を参照のこと。<br>
プルアップ抵抗（R3,R4）は配線の長さに注意すれば省略可である。<br>
J8にタクトスイッチを接続する。例えば、IO43にはスリープ機能を定義してある。<br>
</p>
<!-- p>
<img src="./xiao_esp32s3_i_d.JPG" width="480" height="400"><br>
</p -->
<p>
<img src="./xiao_esp32s3_i_d_board.JPG" width="480" height="600"><br>
</p>
<p><strong>インストール</strong><br>
<ol>
<li>コードを、ZIP形式でダウンロード、適当なフォルダに展開する。</li>
<li>ArduinoIDEにおいて、ライブラリマネージャから以下を検索してインストールする</li>
 <ul>
  <li>Adafruit_BusIO</li>
  <li>Adafruit_GFX</li>
  <li>Adafruit_SSD1306</li>
  <li>RDA5807</li>
 </ul>
<li>追加のライブラリを、ZIP形式でダウンロード、ライブラリマネージャからインストールする</li>
 <ul>
  <li>TimeLib&nbsp;:&nbsp; https://github.com/PaulStoffregen/Time</li>
  <li>Audio　-　audioI2S</li>
 </ul>
<li>ArduinoIDEからxiao_esp32s3_ssd1306_i_d_b_radio_master.inoを開く</li>
<li>「検証・コンパイル」に成功したら、一旦、「名前を付けて保存」を行う</li>
<li>利用するWiFiのアクセスポイントに合わせて、スケッチのssid、passwordを編集する。</li>
<li>ローカルのラジオ局の周波数"stnFreq"と局名"stnName"を設定する。</li>
</ol>
</p>
<p><strong>ブラウザの画面</strong><br>
<p>
操作<br>
<img src="./xiao_esp32s3_i_d_w1.png" width="660" height="360"><br>
</p>
<p>
スケジュール<br>
<img src="./xiao_esp32s3_i_d_w2.png" width="660" height="360"><br>
</p>

<p><strong>注意事項</strong><br>
・一通りの動作は確認していますが、まだ、bugはあると思います。<br>
・動作を保証するものではありませんので、利用の際は、自己責任でお楽しみください。
</p>
