# ZMK Config — Corne Wireless Mechboards — BÉPO

## Hardware

- Clavier : Corne 42 touches (3×6 + 3 pouces), MX Hotswap
- Contrôleur : SuperMini nRF52840 × 2
- Écrans : nice!view (MIP) × 2
- Firmware : ZMK v0.3

## Layout

**BÉPO** sur 4 layers. ZMK envoie des keycodes HID US — **le layout BÉPO doit être activé côté OS**.

### Layer 0 — Base BÉPO

```
┌─────┬─────┬─────┬─────┬─────┬─────┐   ┌─────┬─────┬─────┬─────┬─────┬─────┐
│  W  │  B  │  É  │  P  │  O  │  È  │   │  ^  │  V  │  D  │  L  │  J  │  Z  │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│  Ç  │A/GUI│U/ALT│I/CTL│E/SHF│  ,  │   │  C  │T/SHF│S/CTL│R/ALT│N/GUI│  M  │
├─────┼─────┼─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┼─────┼─────┤
│  $  │  À  │  Y  │  X  │  .  │  K  │   │  '  │  Q  │  G  │  H  │  F  │ ESC │
└─────┴─────┴─────┼─────┼─────┼─────┤   ├─────┼─────┼─────┼─────┴─────┴─────┘
                  │SH/NV│ SPC │BKSP │   │ ENT │ SYM │DL/FN│
                  └─────┴─────┴─────┘   └─────┴─────┴─────┘
```

Homerow mods (balanced, 250ms) : GUI / ALT / CTL / SHF sur la home row.

### Layer 1 — NAV (pouce gauche maintenu)

Flèches vim, Home/End/PgUp/PgDn, Ctrl+Z/X/C/V, Tab/Shift+Tab.

### Layer 2 — SYM (pouce droit)

Chiffres 0–9, symboles prog : `@ | & \ ( ) [ ] { } ~ = < > + - / * # \``

### Layer 3 — FN (pouce droit maintenu)

F1–F12, Bluetooth (BT0/1/2 + CLR), média, Bootloader/Reset.

### Combos

- T + S → Escape
- Space + Enter → Caps Word

## Activer BÉPO côté OS

- **Windows** : Paramètres → Heure et langue → Langue → Ajouter un clavier → Français (BÉPO)
- **macOS** : Préférences Système → Clavier → Méthodes de saisie → + → Français – BÉPO
- **Linux** : `setxkbmap fr bepo` ou via les paramètres clavier de votre DE

## Flash

1. Pusher sur la branche `refresh_mips`
2. GitHub Actions compile automatiquement le firmware
3. Télécharger l'artefact `firmware` depuis l'onglet Actions
4. Extraire les fichiers `.uf2` : `corne_left-nice_nano_v2-zmk.uf2` et `corne_right-nice_nano_v2-zmk.uf2`
5. Pour chaque moitié :
   - Connecter le contrôleur en USB
   - Double-cliquer le bouton reset pour entrer en mode bootloader (le contrôleur apparaît comme clé USB)
   - Copier le `.uf2` correspondant sur le volume monté
   - Le contrôleur redémarre automatiquement

En cas de problème Bluetooth, flasher `settings_reset-nice_nano_v2-zmk.uf2` sur les deux moitiés avant de reflasher le firmware normal.

## Build local (optionnel)

```bash
west build -b nice_nano_v2 -- -DSHIELD="corne_left nice_view_adapter nice_view_gem"
west build -b nice_nano_v2 -- -DSHIELD="corne_right nice_view_adapter nice_view_gem"
```
