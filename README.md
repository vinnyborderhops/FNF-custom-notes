# Character Custom Notes

Standalone Polymod helper for assigning custom notes by current player or opponent.

## Example Mappings

- Opponent `dad` -> `dad-note` -> note style `dad-notes`
- Player `pico-playable` -> `pico-playable-note` -> note style `pico-playable-notes`

The `data/notestyles` files are included, but the mapper waits for the referenced PNG atlases to exist before assigning the custom note kinds.

## Add Opponent Notes

Create a small mapping script under `scripts/modules/note-mapper/`. This example gives opponent `dad` custom notes:

```haxe
import funkin.modding.module.Module;

class DadNoteMapping extends Module
{
  public function new()
  {
    super("note-map-dad", 9999);
    CharacterNoteStyleMapper.mapOpponent("dad", "dad-note", "dad-notes");
    active = false;
  }
}
```

Then add a matching note kind in `scripts/notekinds/`:

```haxe
import funkin.play.notes.notekind.NoteKind;

class DadNoteKind extends NoteKind
{
  public function new()
  {
    super("dad-note", "Dad Notes", "dad-notes");
  }
}
```

Finally add `data/notestyles/dad-notes.json` and its images under `images/notes/dad/`.

## Add Player Notes

Create a mapping script under `scripts/modules/note-mapper/`. This example gives player `pico-playable` custom notes:

```haxe
import funkin.modding.module.Module;

class PicoPlayableNoteMapping extends Module
{
  public function new()
  {
    super("note-map-pico-playable", 9999);
    CharacterNoteStyleMapper.mapPlayer("pico-playable", "pico-playable-note", "pico-playable-notes");
    active = false;
  }
}
```

Then add a matching note kind in `scripts/notekinds/`:

```haxe
import funkin.play.notes.notekind.NoteKind;

class PicoPlayableNoteKind extends NoteKind
{
  public function new()
  {
    super("pico-playable-note", "Pico Playable Notes", "pico-playable-notes");
  }
}
```

Finally add `data/notestyles/pico-playable-notes.json` and its images under `images/notes/pico-playable/`.

## Add Both Sides

Use `mapCharacter` if the same character ID should use the same custom notes as either opponent or player:

```haxe
CharacterNoteStyleMapper.mapCharacter("my-character-id", "my-character-note", "my-character-notes");
```

## Naming Checklist

For each character, keep these three IDs matched:

- Character ID: the engine character ID, like `dad` or `pico-playable`
- Note kind ID: the custom note kind, like `dad-note`
- Note style ID: the JSON filename without `.json`, like `dad-notes`
