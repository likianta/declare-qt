# Declare Qt for Python

`declare-qt` allows you to write QtWidgets in declarative way.

**Before**

```python
from PySide6.QtWidgets import *

app = QApplication()
win = QMainWindow()

btn = QPushButton('CLICK ME', win)
btn.clicked.connect(lambda: print('CLICKED'))

win.show()
app.exec()
```

**After**

```python
from declare_qt.qtwidgets import *

with Application() as app:
    with MainWindow() as win:
        with Button() as btn:
            btn.text = 'CLICK ME'
            btn.clicked.connect(lambda: print('CLICKED'))
        win.show()
    app.exec()
```

## Traits

### New Assignment Style

```python
with Button() as btn:
    btn.text = 'CLICK ME'  # rather than: btn.setText('CLICK ME')
```

### Extend Setting Geometry

```python

with MainWindow() as win:
    
    # ----------------------
    # a new way to set size
    # ----------------------
    
    # get rid of...
    #   widget.setGeometry(widget.x(), widget.y(), width, height)
    #   widget.resize(width, height)
    
    with QWidget() as wid1:
        # style 1
        wid1.width = 100
        wid1.height = 80
    
    with QWidget() as wid2:
        # style 2
        wid2.size = (100, 80)
    
    # --------------------------
    # a new way to set position
    # --------------------------
    
    # get rid of...
    #   widget.setGeometry(x, y, widget.width(), widget.height())
    #   widget.move(x, y)
    
    with QWidget() as wid3:
        # style 1
        wid3.x = 100
        wid3.y = 80
    
    with QWidget() as wid4:
        # style 2
        wid4.position = (100, 80)

```

### Dynamic Bindings

We have new mechanism to bind dynamic properties to QtWidgets -- it is called
"kiss" and "bind".

```python
with MainWindow() as win:
    win.width = 100
    win.height = 80
    
    with Button() as btn:
        btn.width.kiss(win.width)
        #         ^^^^
        #   this is equal to: btn.width = win.width
        
        btn.height.bind(win.height)
        #          ^^^^
        #   this is equal to a complicated implementation:
        #       class MainWindow(QMainWindow):
        #           resized = Signal(int, int)
        #           def resizeEvent(self, event):
        #               super().resizeEvent(event)
        #               self.resized.emit(event.size().width(), 
        #                                 event.size().height())
        #       win = MainWindow()
        #       btn = Button()
        #       win.resized.connect(lambda w, h: btn.setWidth(w))
        
        #   reference link: 
        #       https://stackoverflow.com/questions/43126721/detect-resizing-in
        #       -widget-window-resized-signal
```

### Easy to Create Animations

*Note: this is in concept.*

```python
with QLabel() as label:
    label.text = 'move from left to right'
    label.x.set_anim(
        start=0,
        end=100,
        duration=1000,
        easing=QEasingCurve.OutQuad
    )
    
    # rather than:
    #   anim = QPropertyAnimation(label, 'x')
    #   anim.setStartValue(0)
    #   anim.setEndValue(100)
    #   anim.setDuration(1000)
    #   anim.setEasingCurve(QEasingCurve.OutQuad)
    #   label.xChanged.connect(anim.start)
    #   #   note that label.xChanged is not support by default, we have to 
    #   #   implement this signal by ourselves, see example above. 
```

## Install

This project is not ready to provide PyPI package.

You can clone this repository and try yourself:

```
git clone https://github.com/likianta/declare-qt.git
```

*Note: the minimum required Python version is 3.8.*

## Usage

*TODO*
