# japanese_text_to_speech

日本語テキストを音声として出力する ROS node です．

[Open JTalk](http://open-jtalk.sourceforge.net/) を利用しています．

## インストール

Open JTalkとaplayコマンドに依存しています．

```
sudo apt install open-jtalk open-jtalk-mecab-naist-jdic hts-voice-nitech-jp-atr503-m001 alsa-utils
```

catkin workspace内に設置して `catkin_make` してください．

## 使い方

`japanese_text_to_speech` node を起動してください．
この node がサーバとなり，クライアントから受け取ったテキストを音声出力します．

```
rosrun japanese_text_to_speech japanese_text_to_speech
```

この node は [actionlib](http://wiki.ros.org/actionlib) を使って実装されています．
簡単なクライアントのサンプルとして `test_client` nodeを用意してあります．

```
rosrun japanese_text_to_speech test_client
```

### 音声モデルの切り替え

デフォルトでは男性の音声を使うようになっていますが，他の音声に切り換えることもできます．

`.htsvoice` ファイルを適当な場所に設置し， `~hts_voice_file` rosparam をセットしてください．

```
rosrun japanese_text_to_speech japanese_text_to_speech _hts_voice_file:='/path/to/htsvoice'
```

#### メイ＆タクミ

例えば，名古屋工業大学の開発する[メイ＆タクミ](https://mei.web.nitech.ac.jp)の音声モデルを利用できます．

以下のコマンドで，音声モデルを取得し，展開します．

```bash
wget https://sourceforge.net/projects/mmdagent/files/MMDAgent_Example/MMDAgent_Example-1.8/MMDAgent_Example-1.8.zip
unzip MMDAgent_Example-1.8.zip
```

展開したファイルの`Voice/`以下にあるファイルを指定することにより，音声モデルを利用できます．
例えば，メイの幸せな声の音声モデルを利用する場合は，次のように引数を追加します．

```bash
rosrun japanese_text_to_speech japanese_text_to_speech _hts_voice_file:='PATH_TO_UNZIPPED_FILES/MMDAgent_Example-1.8/Voice/mei/mei_happy.htsvoice'
```

参考：https://www.rcnp.osaka-u.ac.jp/~kohda/linux/espeak.html
