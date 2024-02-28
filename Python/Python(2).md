2024-02-28 (수)
<hr>


> [!note] pyqt03

```python
import sys
from PyQt5 import uic
from PyQt5.QtWidgets import QApplication, QMainWindow
form_class = uic.loadUiType("./pyqt03.ui")[0]

class WindowClass(QMainWindow, form_class):
	def __init__(self):
		super().__init__()
		self.setupUi(self)
		self.btn.clicked.connect(self.btnClick)
	
	def btnClick(self):
		s1 = self.pte01.toPlainText()
		s2 = self.pte02.toPlainText()
		is1 = int(s1)
		is2 = int(s2)
		mul = is1 * is2
		self.pte03.setPlainText(str(mul))

if __name__ == "__main__":
	app = QApplication(sys.argv)
	myWindow = WindowClass()
	myWindow.show()
	app.exec_()
```

`QPlainTextEdit` 값 가져오기, 내보내기 : toPlainText(), setPlainText()


>[!tip]
>self : 전역변수

<hr>

