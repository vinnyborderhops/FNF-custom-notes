# Character Custom Notes

Standalone Polymod helper for assigning custom notes by current player or opponent.

## Example Mappings

- Opponent `dad` -> `dad-note` -> note style `dad-notes`
- Opponent `senpai` -> `senpai-note` -> note style `senpai-notes`
- Player `pico-playable` -> `pico-playable-note` -> note style `pico-playable-notes`
- Player `pico-pixel` -> `pico-pixel-note` -> note style `pico-pixel-notes`

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

## Add Pixel Opponent Notes

Pixel note styles should inherit from the engine `pixel` note style, not `funkin`, so missing values keep the correct scale, offsets, and pixel rendering flags. This example gives opponent `senpai` custom pixel notes:

```haxe
import funkin.modding.module.Module;

class SenpaiNoteMapping extends Module
{
  public function new()
  {
    super("note-map-senpai", 9999);
    CharacterNoteStyleMapper.mapOpponent("senpai", "senpai-note", "senpai-notes");
    active = false;
  }
}
```

Then add a matching note kind in `scripts/notekinds/`:

```haxe
import funkin.play.notes.notekind.NoteKind;

class SenpaiNoteKind extends NoteKind
{
  public function new()
  {
    super("senpai-note", "Senpai Notes", "senpai-notes");
  }
}
```

Finally add `data/notestyles/senpai-notes.json` and its images under `images/notes/senpai/`.

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

## Add Pixel Player Notes

Pixel note styles should inherit from the engine `pixel` note style, not `funkin`, so missing values keep the correct scale, offsets, and pixel rendering flags. This example gives player `pico-pixel` custom pixel notes:

```haxe
import funkin.modding.module.Module;

class PicoPixelNoteMapping extends Module
{
  public function new()
  {
    super("note-map-pico-pixel", 9999);
    CharacterNoteStyleMapper.mapPlayer("pico-pixel", "pico-pixel-note", "pico-pixel-notes");
    active = false;
  }
}
```

Then add a matching note kind in `scripts/notekinds/`:

```haxe
import funkin.play.notes.notekind.NoteKind;

class PicoPixelNoteKind extends NoteKind
{
  public function new()
  {
    super("pico-pixel-note", "Pico Pixel Notes", "pico-pixel-notes");
  }
}
```

The included `data/notestyles/pico-pixel-notes.json` uses `"fallback": "pixel"` and references copied stock pixel assets under `images/notes/pico-pixel/`:

- `notes.png` / `notes.xml`
- `hold.png`
- `splashes.png` / `splashes.xml`
- `hold-cover.png` / `hold-cover.xml`

Use this as the template for custom pixel note styles. Keep pixel-specific values like `scale`, `isPixel`, `noteStrumline.offsets`, `holdNote.offsets`, `noteSplash.offsets`, and `holdNoteCover.offsets` in the JSON when replacing the art.

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
- Pixel styles: use `"fallback": "pixel"` and put the atlas files under `images/notes/<your-id>/`
