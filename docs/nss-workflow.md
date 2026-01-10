# NSS — workflow operatorski (1 ekran)

## Zasada nadrzędna

**Najpierw sprawdzasz, potem uruchamiasz, na końcu zmieniasz system.**

VM jest **bramką bezpieczeństwa** przed `switch`.

---

## Ścieżka pracy (mentalny model)

EDYCJA  
→ build  
→ build-vm  
→ (VM OK?)  
→ nss → switch

---

## 1. Edycja konfiguracji

Zmiany w systemie robisz w:

/etc/nixos

(np. `configuration.nix`, moduły, home-manager, flakes)

---

## 2. Build — „czy to się w ogóle buduje?”

Sprawdzenie składni i zależności, **bez zmian w systemie**.

````bash
nixos-rebuild build --flake /etc/nixos#$(hostname)
✔ wykrywa błędy Nix

❌ nie uruchamia systemu

❌ nie robi switch

3. Build-VM — „czy ten system DZIAŁA?”
Buduje i uruchamia ten sam system w maszynie wirtualnej.

bash
Skopiuj kod
nixos-rebuild build-vm --flake /etc/nixos#$(hostname)
./result/bin/run-*-vm
Sprawdź minimum:

system bootuje

systemd wstaje

login / shell działa

Jeśli VM nie wstaje → NIE ROBISZ SWITCH.

4. NSS — świadoma decyzja na hoście
bash
Skopiuj kod
nss
Poziom 1: decyzja
N — NIC nie zmieniać w systemie

S — ZMIENIĆ system (switch)

Poziom 2: tryb
N — bez zmian w systemie

A — build

V — build-vm

S — zmienia system

B — build + switch

C — build + switch + commit + push

Złote reguły
Zawsze VM przed switchem

switch robisz tylko, gdy widziałeś system działający

nss ma pytać — Ty decydujesz

Jedno zdanie do zapamiętania
Jeśli system wstał w VM, to host też wstanie.

yaml
Skopiuj kod

---

## ✅ Co teraz zrobić

```bash
cd /home/michal/test-sterile
mkdir -p docs
nvim docs/nss-workflow.md
````
