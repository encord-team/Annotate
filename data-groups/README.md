## How do use these examples

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
