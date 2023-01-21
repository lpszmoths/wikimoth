---
title: Godot
summary: Godot snippets
---

## Project setup

1. Download and install [godot-next](https://github.com/godot-extended-libraries/godot-next/)
1. Download and install _insert gizmos plugin here_

## Project structure

```
res://
|-- addons/
|-- tests/
|-- util/
|-- default_env.tres
'-- icon.png
```

## Making custom editors

```
tool
extends Node

const CustomPropertyEditor = preload("res://path/to/custom-property-editor.gd")

func _parse_begin(editor: EditorInspectorPlugin):
    var button: Button = InspectorControls.new_button(
        "Button label",
        is_toggle,
        self,
        "_on_button_click"
    )
    editor.add_custom_control(button)

func _parse_category(
    editor: EditorInspectorPlugin,
    category_name: String):
    if not category_name == 'Script properties':
        return
    var button: Button = InspectorControls.new_button(
        "Button label",
        is_toggle,
        self,
        "_on_button_click"
    )
    editor.add_custom_control(button)

func _parse_property(
    editor: EditorInspectorPlugin,
    info: PropertyInfo
):
    var name = info.name
    var hint = info.hint
    var hint_string = info.hint_string
    var type = info.type

    if info.name == 'my_prop_name':
        var prop_editor: EditorProperty = CustomPropertyEditor.new()
        editor.add_property_editor(
            'my_prop_name',
            prop_editor
        )

    # Returning true removes the built-in editor
    # for this property, otherwise allows to insert
    # a custom editor before the built-in one.
    # Returning true removes the built-in editor
    # for this property, otherwise allows to insert
    # a custom editor before the built-in one.
    return false


func _parse_end(editor: EditorInspectorPlugin):
    var button: Button = InspectorControls.new_button(
        "Button label",
        is_toggle,
        self,
        "_on_button_click"
    )
    editor.add_custom_control(button)
```

## Making custom gizmos

TODO
