---
layout: post
title: PySide2 demo
subtitle: using OpenGL
bigimg: /img/dmitri-popov-69420-unsplash.png
tags: [python, visualization]
---

QT is used for building desktop applications that run on all major platforms (Linux, Mac, Win). QT is implemented in C++ for C++ developers. Recently they put a lot of effort into making the tools available for Python developers, too. This is named PySide2 or "QT for Python." The abstractions are very similar to PyQT5 (if you happen to know these).

QT is well documented for the C++ part including samples. For PySide2 the documentation is a bit lacking (which is expected for new tools). I thought it might be a good idea to add a sample to demo some of the features:

![Hello OpenGL sample](/media/pyside2_opengl/hello_opengl.gif){: width=416}

About 200 lines of code to create a desktop application with 3d rendering is great. Don't you think?

When using PySide2 you do not need to compile the UI after every change... Not having to wait for the compiler any more makes QT application development attractive since development speed gets as good as web application development.

As you can see from the following snippet building a UI from std. widgets or custom ones is straight forward:

``` python
class MainWindow(QtWidgets.QMainWindow):
    def __init__(self):
        super().__init__()

        central_widget = QtWidgets.QWidget()
        self.setCentralWidget(central_widget)

        self.glWidget = GLWidget()
        ...

        # sliders
        x_slider = self.create_slider(self.glWidget.x_rotation_changed,
                                     self.glWidget.set_x_rot_speed)
        y_slider = self.create_slider(self.glWidget.y_rotation_changed,
                                     self.glWidget.set_y_rot_speed)
        z_slider = self.create_slider(self.glWidget.z_rotation_changed,
                                     self.glWidget.set_z_rot_speed)

        # set the layout
        central_layout = QtWidgets.QVBoxLayout()
        central_layout.addWidget(self.glWidgetArea)
        central_layout.addWidget(x_slider)
        central_layout.addWidget(y_slider)
        central_layout.addWidget(z_slider)
        central_widget.setLayout(central_layout)

        x_slider.setValue(1)
        y_slider.setValue(1)
        z_slider.setValue(0)

        self.setWindowTitle("Hello OpenGL")
        self.resize(400, 300)
```

I included the full source code (see resources below).

Best,
Mark

## Resources
* [opengl_tutorial.py full sample code](https://gist.github.com/markfink/4f8d6b8271d9cd865528d437d129e072)
* [Transformations in OpenGL](https://www.cs.cmu.edu/afs/cs/academic/class/15462-s09/www/lec/03/lec03a.pdf)
* [PySide2 official getting started](https://doc.qt.io/qtforpython/gettingstarted.html)
* [PySide2 Webinar Slides](https://www.slideshare.net/ICSinc/qt-for-python)
* [PySide2 getting started](http://www.blog.pythonlibrary.org/2018/04/18/getting-started-with-qt-for-python/)
