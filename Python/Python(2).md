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

> [!note] 전화기 만들기(내버전)

```python
import sys

from PyQt5 import uic
from PyQt5.QtWidgets import QApplication, QMainWindow
from PyQt5.Qt import QMessageBox

form_class = uic.loadUiType("./pyqt07.ui")[0]

class WindowClass(QMainWindow, form_class):
	def __init__(self):
		super().__init__()
		self.setupUi(self)
		self.pb_call.clicked.connect(self.btnClick)
		self.pb0.clicked.connect(self.btnClick0)
		self.pb1.clicked.connect(self.btnClick1)
		self.pb2.clicked.connect(self.btnClick2)
		self.pb3.clicked.connect(self.btnClick3)
		self.pb4.clicked.connect(self.btnClick4)
		self.pb5.clicked.connect(self.btnClick5)
		self.pb6.clicked.connect(self.btnClick6)
		self.pb7.clicked.connect(self.btnClick7)
		self.pb8.clicked.connect(self.btnClick8)
		self.pb9.clicked.connect(self.btnClick9)
		self.txt = "";

	def btnClick(self):
		QMessageBox.about(self,"calling....",self.le.text())
	
	def btnClick0(self):
		self.txt += "0"
		self.le.setText(self.txt)
	def btnClick1(self):
		self.txt += "1"
		self.le.setText(self.txt)
	def btnClick2(self):
		self.txt += "2"
		self.le.setText(self.txt)
	def btnClick3(self):
		self.txt += "3"
		self.le.setText(self.txt)
	def btnClick4(self):
		self.txt += "4"
		self.le.setText(self.txt)
	def btnClick5(self):
		self.txt += "5"
		self.le.setText(self.txt)
	def btnClick6(self):
		self.txt += "6"
		self.le.setText(self.txt)
	def btnClick7(self):
		self.txt += "7"
		self.le.setText(self.txt)
	def btnClick8(self):
		self.txt += "8"
		self.le.setText(self.txt)
	def btnClick9(self):
		self.txt += "9"
		self.le.setText(self.txt)
	
	if __name__ == "__main__":
		app = QApplication(sys.argv)
		myWindow = WindowClass()
		myWindow.show()
		app.exec_()
```


> [!note] 전화기 만들기(선생님 버전)



```python

```

