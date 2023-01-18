The goal is to remove lines with "name1", "name3", or "name5". If the line is preceded by an XML comment, we want to remove that line as well.

This produces incorrect output (the first comment should be removed):

```bash
comby -config "item-both.toml" -f item-test.xml -matcher .xml -stdout -match-newline-at-toplevel
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources xmlns:tools="http://schemas.android.com/tools">
    <!-- this is a comment -->

    <!-- this is another comment -->
    <item name="name2">value2</item>


    <item name="name4">value4</item>
</resources>
```

This produces correct output:

```bash
comby -config "item-with-comment.toml,item-without-comment.toml" -f item-test.xml -matcher .xml -stdout -match-newline-at-toplevel
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<resources xmlns:tools="http://schemas.android.com/tools">

    <!-- this is another comment -->
    <item name="name2">value2</item>


    <item name="name4">value4</item>
</resources>
```