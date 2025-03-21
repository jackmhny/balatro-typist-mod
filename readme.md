<!-- markdownlint-disable line-length -->
# Typist mod for Balatro

<p align="center">
  <img src="https://raw.githubusercontent.com/janw4ld/balatro-typist-mod/main/assets/typist-joker-hd.png" alt="Typist logo, a modification of Four Fingers that's square in aspect ratio and has five fingers instead" style="width:50%;">
</p>

this mod is a mostly complete implementation of keyboard driven UX for Balatro. it adds keybindings for all of the gameplay actions, and includes code from [DorkDad141's Keyboard Shortcuts](https://github.com/DorkDad141/keyboard-shortcuts) & [FlushHotkeys](https://github.com/Agoraaa/FlushHotkeys), which adds keybindings for quickly selecting the best hand available or making flush & high card hands -called "the cheat layer" in typist-, but no hands are ever played or discarded automatically by the mod, it just picks cards and you can inspect the hand & modify it before playing it with `space` or discarding it with `tab`

## video demo

[![YouTube](http://i.ytimg.com/vi/k2l6-RqTk1c/hqdefault.jpg)](https://www.youtube.com/watch?v=k2l6-RqTk1c)

## installation

the only dependency is the `lovely` code injector, which is also a dependency of the [Steamodded mod loader](https://github.com/Steamodded/smods), so if you have `smods` you can just drop this repo into your `Mods` directory and it'll get picked up. if not then follow the first two steps of Steamodded's ["How to install Steamodded" guide](https://github.com/Steamodded/smods/wiki#how-to-install-steamodded), namely "Step 1: Anti-virus setup" and "Step 2: Installing Lovely", then download the mod (either with `git clone` or from the green "Code" button at the top of the page) and save it to the appropriate directory for your platform:

- windows: `%AppData%/Balatro/Mods`
- mac: `~/Library/Application Support/Balatro/Mods`
- linux+wine/proton: `~/.local/share/Steam/steamapps/compatdata/2379780/pfx/drive_c/users/steamuser/AppData/Roaming/Balatro/Mods`

## compatibility

game versions:

- `1.0.1n`
- `1.0.1o`


other mods:

- V-rtualized/BalatroMultiplayer [v0.1.8.4](https://github.com/V-rtualized/BalatroMultiplayer/releases/tag/0.1.8.4),  [v0.2.1](https://github.com/V-rtualized/BalatroMultiplayer/releases/tag/0.2.1) and the private 1.0 alpha
  - on pvp blinds `space` toggles the ready state instead of immediately starting the blind
  - in lobby menu `space` starts the run (if you're the host)
- Amvoled/Taikomochi revs [`9a99c3a`](https://github.com/Amvoled/Taikomochi/tree/9a99c3a12c11573a5a16d9b6c11737307d3d25d8) & [`26d2507`](https://github.com/Amvoled/Taikomochi/tree/26d250746a45f1265168324f16c6a62f0050c461)
  - `enter` on the game over screen retries the last ante for zen mode runs
- [Agoraaa/FlushHotkeys `4c0b1df`](https://github.com/Agoraaa/FlushHotkeys)
  - removes FlushHotkeys keyboard shortcuts to prevent conflicts
  - uses FlushHotkeys `select_best_hand` implementation instead of mine (will be removed in the future)

## feature overview

- toggling hand cards with `asdfgh...` keys
- a complete implementation of every action in every game state, with
  - `space` being generally the "proceed" button:
    - it plays the selected hand
    - selects the upcoming blind
    - uses consumable cards
    - selects the highlighted pack item
    - starts a new run from the game over screen
  - `tab` being the dismiss button:
    - it discards the selected hand
    - moves from the shop to blind selection
    - sells consumable or joker cards
    - skips the current booster pack
    - closes any overlay menu
    - exits to main menu from the game over screen
  - the bottom row of the keyboard as the "control panel", for example:
    - in rounds:
      - hold `z` for the quick deck preview
      - press `c` to sort by suit
      - `v` to sort by rank
      - `b` to sort by enhancement+score, where glass cards are moved to the end, and lucky and mult cards to the beginning
    - in the shop:
      - `c` to buy an item or a pack or a voucher
      - `v` to buy and use an item, or buy a pack or a voucher
    - `n` to deselect all cards in a cardarea and `m` to invert card selection in rounds
    - `x` to view run info whenever it's available
    - & others (see [`./mod/layout.lua`](./mod/layout.lua)) for dvorak and the full keymap
  - mnemonic keys for less frequent actions, like `s` to skip blinds, `r` to reroll the shop or boss, `b` in the cheat layer (accessed by holding `p`) to pick the best hand out the available cards, `f` in the cheat layer to fish for the best flush in hand, etc
- cardarea keybind layers for selecting, moving, selling & using cards. these apply globally for
  - consumables, accessed by holding `'`
  - jokers, accessed by holding `[`
  - pack cards, with no leader key
  - the shop, with no leader key
  - the hand, which is accessed
    - by holding `/` everywhere for selection and movement of a single card
    - by holding `shift+/` for multiselect in booster packs
    - with no leader key for multiselect in rounds
- support for `qwerty` and `dvorak` keyboard layouts, where positional keys are kept consistent across both layouts and mnemonic keys aren't changed. (e.g. `asdf` to toggle the first four cards in qwerty translates to `aoeu` in dvorak, but `r` to reroll the shop or the boss blind stays `r` in both layouts)
- support for keybind overrides, so you can change the default keybinds to your liking
- any key to skip the splash screen and `space` to click any "play" or "continue" button, so a run can be started from game launch until the first blind with the `space` button only

## TODOs

- deck selection keybinds, the "new run" menu has only one keybind, `space` to start a run with the selected deck, would be nice to add `hjkl` for deck and stake selection too

## future plans

- half-keyboard layouts to be used with one hand on the mouse and the other on one side of keyboard (similar to photoshop and other editing software)
- menu navigation keybinds, menus are the only part of the game that currently requires the mouse to navigate
- redesign arcana and spectral packs UX, hand manipulation in these screens is a bit clunky due to the need for `shift+/` for cardarea multiselect
- use the controller UI to display keybind hints  
  ![controller hints UI, shows the game's discard button with a "Y" written on it](https://raw.githubusercontent.com/janw4ld/balatro-typist-mod/main/assets/controller-hints.png)
