---
title: Godot
summary: Godot snippets
---

## Project setup

1. Download and install [godot-next](https://github.com/godot-extended-libraries/godot-next/)
1. Download and install _insert gizmos plugin here_

## Finding the current camera

```
get_viewport().get_camera()
```

## Is in editor?

```
if Engine.editor_hint:
    # editor code
```

## Instantiating packed scenes

```
const MyPrefab = preload("res://path/to/prefab.tscn")

var child = MyPrefab.instance()
add_child(child)
```

## Raycasting downward

```
var raycast: RayCast = RayCast.new()
raycast.transform.origin = Vector3(x, y, z)
raycast.cast_to = Vector3(0, -1, 0) # default
var collision_point: Vector3 = raycast.get_collision_point()
var collision_normal: Vector3 = raycast.get_collision_normal()
var collider: Object = get_collider()
```

## Throwing errors/exceptions

```
printerr("Error")
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
