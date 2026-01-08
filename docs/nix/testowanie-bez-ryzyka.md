# Jak testować zmiany NixOS bez ryzyka

## Zasada

Nigdy nie testuj bezpośrednio w `/etc/nixos`.
Test = build bez switcha na kopii.

## Procedura

1. LAB: edytuj w repo
2. Test:
   - `nss-check` (build bez switcha)
3. Jeśli OK:
   - skopiuj wybrane pliki do `/etc/nixos`
   - `nss`

## Skrót mentalny

LAB → test (build) → PROD → switch
