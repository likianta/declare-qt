# Conceptual Implementation

## Property Binding

__Expectation__

```python
# simple binding to B.width.
A.width.bind(B.width)

# binding to B.width, but with an expression.
A.width.bind(B.width + 10)

# binding to multiple notifiers, with an expression.
A.width.bind(B.width or C.width)
```

__Base Implementation__

```python
# assume we have implemented a signal -- `widthChanged` -- to QWidget that 
# captures its width change event.

A = QWidget()
B = QWidget()

B.widthChanged.connect(lambdex('w', """
    A.resize(w, A.height())
"""))

```

## Easy Animation

__Expectation__

```python
# set animation on behavior.
A.width.set_anim(
    duration=1000,
    easing=easing.OUT_QUAD,
    on_complete=lambda: print('done')
)
```

This idea is inspired by QML Behavior:

```qml
Item {
    Behavior on width {
        NumberAnimation {
            duration: 1000
            easing.type: Easing.OutQuad
        }
    }
}
```

__Base Implementation__

```python
animation = 
```

