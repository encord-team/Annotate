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

## Carousel metadata preview

When using a `data_unit_list` tile (carousel), you can display each item's file metadata as an overlay when the annotator hovers over it. Set `hoverMetadata` on the carousel tile to enable this:

```json
{
  "layout": {
    "type": "data_unit_list",
    "keys": ["scan1", "scan2", "scan3"],
    "hoverMetadata": {
      "keys": ["patient_id", "study_date", "modality"]
    }
  }
}
```

- **`keys`** — the list of `client_metadata` keys to show. Omit (or set to `null`) to show all available metadata for the file.
- Values that are too long to fit in the tile are truncated with an ellipsis.

See [`examples/carousel-with-metadata.json`](examples/carousel-with-metadata.json) for a full example.

You can also enable metadata preview on individual tiles via `TileSettings.hoverMetadata` inside `settings.tileSettings`.
