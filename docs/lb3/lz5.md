# Testing


## Systemtest

```
# Installation stress-ng, falls nicht schon installiert
sudo apt-get install stress-ng

# 4 Worker starten die die CPU stressen mit verschiedenen Methoden, für 60s
stress-ng --cpu 4 --timeout 60s

# 2 Worker starten die die Disk stressen mit Lesen/Schreiben/Löschen von Daten, für 60s
stress-ng --hdd 2 --timeout 60s

# ...das ganze mit IO (Buffer Cache jeweils commiten)
stress-ng --hdd 2 --io 2 --timeout 60s

# 2 Worker für Memory Stress - jeweils mit der Anzahl Bytes, für 60s
stress-ng --vm 2 --vm-bytes 256M --timeout 60s

# Das Ganze kann man jetzt auch kombinieren
stress-ng --cpu 4 --io 2 --vm 1 --vm-bytes 256M --timeout 200s
```