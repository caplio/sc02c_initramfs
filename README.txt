sakuramilkさん作成のデュアルブート用initramfsを自分向けカスタマイズしたものです。

■仕様

【1st ROM】

・mountするパーティション含めて全て標準仕様
・純正カーネルでの使用を想定


【2nd ROM】

・/data領域は、/xdata/data1へ保存されます（FR時はここを削除
・/system は、hidden領域を使用します。（/dev/block/mmcblk0p12）

■2nd側へのROMの展開

ROMのupdater-scriptを以下の内容で修正する必要があります。

　- mmcblk0p9をmmcblk0p12に変更
　- mmcblk0p5へのカーネル書き込み部分を削除
　- その他影響がありそうな内容を削除
　
■ROMの切り替え

/data/boot.confへ「secondary」の文字列を記入
2nd ROM状態で再起動を行うと、自動的に1stのROMに戻ります
（2nd ROMの問題発生時は、再起動してみてください）
　
■懸念事項

リカバリーからFRをすると2nd側も消える（はず
2ndだけ消したい場合は、/data/data1を消す

sdcard上のデータは競合する可能性がある。
Dalvik cacheなどで同じアプリを使っていると
不具合が出る可能性？

CWMでのバックアップは、2nd ROM側の/systemはバックアップされない。
/dataは全部取るので容量に注意。