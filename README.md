**Polskie pliki dźwiękowe (tylko część obsługi radiowej nie całego Asterisk)**

Pliki polskie nie zastępują oryginalnych plików ASL3 tylko jeśli są wgrane to są używane
zamiast oryginalnych

**INSTLACJA**

```
sudo -s
apt install -y git
cd /usr/local/share/asterisk/sounds
git clone https://github.com/radioprj/ASL-sound-pl.git
chown -R asl:asl rpt/ letters/ digits/ phonetic/
systemctl restart asterisk
```
**AKTUALIZACJA**

```
sudo -s
cd /usr/local/share/asterisk/sounds
git push
```

Jeśli nie spodobały Ci się wersje polskie i chcesz wrócić do oryginalnych wystarczy że usuniesz
Pliki polskie i będziesz używał oryginalne:

**USUWANIE**
```
sudo -s
cd /usr/local/share/asterisk/sounds/
rm -rf rpt/ letters/ digits/ phonetic/
systemctl restart asterisk
```


Pliki zostały zrobione przy pomocy [piper-tts](https://github.com/rhasspy/piper) z modelem głosowym [pl_PL-zenski_wg_glos-medium.onnx
](https://huggingface.co/WitoldG/polish_piper_models/tree/main)

Jeśli chcesz poprawić jakiś plik, należy zrobić:

```

echo "Treść nagrania" | piper --model pl_PL-zenski_wg_glos-medium.onnx --output_file temp.wav 2>/dev/null

# Konwersja na ULAW gdzie nazwa_pliku.ulaw musi być taka sama jak który chcemy poprawić
ffmpeg -y -i temp.wav -ar 8000 -ac 1 -filter:a "volume=0.7" -acodec pcm_mulaw -f mulaw "nazwa_pliku.ulaw" 2>/dev/null

# skopiować nazwa_pliku.ulaw do odpowiedniego katalogu

```

**Używasz na własną odpowiedzialność i autor nie ponosi odpowiedzialności za wykorzystane rozwiązanie i wynikające z niego skutki.**
