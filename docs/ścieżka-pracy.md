EDYCJA
→ nixos-rebuild build
→ nixos-rebuild build-vm
→ jeśli VM OK:
nss → switch

📌 ŚCIĄGA OPERATORSKA — NixOS (1 ekran)

Zasada nadrzędna:
Najpierw sprawdzasz, potem uruchamiasz, na końcu przełączasz hosta.

EDYCJA
↓
nixos-rebuild build
↓
nixos-rebuild build-vm
↓
(test w VM)
↓
nss → switch

1️⃣ EDYCJA
sudo nvim /etc/nixos/nixos/configuration.nix

Zmiany w:

services

pakietach

home-manager

shell / env

modułach

2️⃣ BUILD — „czy to się w ogóle buduje?”
nixos-rebuild build --flake /etc/nixos#$(hostname)

✔ sprawdza składnię i zależności
❌ nie zmienia systemu
❌ nie uruchamia niczego

3️⃣ BUILD-VM — „czy ten system DZIAŁA?”
nixos-rebuild build-vm --flake /etc/nixos#$(hostname)
./result/bin/run-\*-vm

✔ system bootuje
✔ usługi startują
✔ login / shell działa

Jeśli VM nie wstaje → NIE ROBISZ SWITCH

4️⃣ NSS — host (świadoma decyzja)
nss

A – build → jeszcze bez zmian

V – build-vm → ostatni test bezpieczeństwa

B – switch → zmiana systemu

C – switch + commit + push

🧠 Jedno zdanie do zapamiętania

VM jest bramką bezpieczeństwa przed switchem.

To jest cała filozofia.
