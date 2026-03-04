## How to use these examples

1. Copy the `.json` files in the examples folder and replace `<storage_item_id>` with the IDs of the files you want to group. You can find the IDs in the Encord app or by using `list_items()` on a folder:

   ```python
   folder = client.get_storage_folder("<folder_id>")
   storage_items = folder.list_items()
   ```

1. Use `create_data_group()` to create a data group:

   ```python
   import json
   from encord.orm.storage import DataGroupCustom

   folder = client.get_storage_folder("<folder_id>")
   with open("path/to/example.json", "r") as file:
       data = json.load(file)
   group_input = DataGroupCustom.from_dict(data)

   folder.create_data_group(group_input)
   ```

## Settings reference

### `settings.labelPanel`

Controls the behaviour of the left-hand label panel in the label editor.

| Field | Type | Default | Description |
|---|---|---|---|
| `showAllTiles` | boolean | `false` | When `true`, the label panel shows annotations from **all tiles** in the data group as a flat list, instead of only the currently active tile. Hovering a label in the panel highlights it on the canvas, and vice versa. Clicking a label on a video data unit navigates to the frame the label belongs to. |

**Example**

```json
{
  "settings": {
    "labelPanel": {
      "showAllTiles": true
    }
  }
}
```

See [`examples/dicom-study-cross-tile-labels.json`](examples/dicom-study-cross-tile-labels.json) for a complete example using a four-tile mammography study.

### `settings.tileSettings`

Per-tile display settings, keyed by the tile's key in `layoutContents`.

| Field | Type | Default | Description |
|---|---|---|---|
| `title` | string \| null | `null` | Optional title displayed in the tile toolbar. |
| `isReadOnly` | boolean | `false` | When `true`, the tile cannot be annotated. |

### `settings.fixedLayout`

Set to `true` to prevent annotators from adding, removing, or rearranging tiles. Defaults to `false`.
