# Architecture document

## Actors folder

It contains actors like hero, ennemis or characters. They can be controlled
by players but they can also be controlled by the game itself.

- **Actor** is located at the root of `actors/` folder
- sub-classes of it are arranged in sub-folders

## Assets folder

It contains assets like Audios, Fonts or Images which are actually used in the game.

## Objects folder

...

## Resources folder

### Resources/Localization

One group of files for each part of the game. For instance, menus will use `MenuTranslations` files.

- `.xlsx` in the source of truth, the only one to be modified
- `.csv` is generated form the `xlsx` (in UTF-8)
- other files are generated by Godot

### Resources/Theme

Themes which may be used multiple times in the game.

- `MenuTheme` is to be used for menus.

## Scenes folder

Contains scenes like levels and menus.

### Console scene

The `GameConsole` is a UI for developers which allows to enter commands for debugging.
By default, on an AZERTY it opens when typing the "²" key.

To add it to a scene, add the `GameConsole` to it, and add `Command` children nodes.
Every `Command` nodes have to be configured to **target** an existing node of the scene,
onto an existing **function** with the right **parameters**.

To define a parameter there are 2 formats:
- `name:type` if parameter is mandatory (eg: `time:float`);
- `name:type:default` if parameter is optional, optionals must be last parameters (eg: `time:float:0.8`).

Allowed types are: `string`, `int` or `float`.

## Services folder

### Save / ProgressionService

Autoloaded script to use to store and load progression of the player.
Make sure `ProgressionService.init()` is called while starting the game.

Use:
- `ProgressionService.data`: to get the current value of Progression
- `ProgressionService.save(progression: Progression)`: to save the given progression

To change the values to save you'll have to change:
- `ProgressionService._serialize()` method which serializes the progression object
- `ProgressionService._parse()` method which parses the saved value
- `Progression` class which is the structured data
