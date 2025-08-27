# Ejercicio1
import sys
from PyQt5.QtWidgets import (QApplication, QWidget, QLabel, QLineEdit, QGridLayout, 
                             QRadioButton, QButtonGroup, QComboBox, QCheckBox, 
                             QPushButton, QMessageBox)
from PyQt5.QtGui import QFont
from PyQt5.QtCore import Qt

class Ventana(QWidget):
    def __init__(self):
        super().__init__()
        #título
        self.setWindowTitle('Formulario de Registro')
        self.setGeometry(100, 100, 400, 300)
        
        layout = QGridLayout()
        self.setLayout(layout)

        # Etiqueta del título
        titulo = QLabel('Formulario de Registro')
        titulo.setFont(QFont('Arial', 16, QFont.Bold))
        titulo.setAlignment(Qt.AlignCenter)
        layout.addWidget(titulo, 0, 0, 1, 3)

        # Nombre
        lbl_nombre = QLabel('Nombre:')
        layout.addWidget(lbl_nombre, 1, 0)
        self.txt_nombre = QLineEdit()
        layout.addWidget(self.txt_nombre, 1, 1, 1, 2)

        # Email
        lbl_email = QLabel('Email:')
        layout.addWidget(lbl_email, 2, 0)
        self.txt_email = QLineEdit()
        layout.addWidget(self.txt_email, 2, 1, 1, 2)

        # Contraseña
        lbl_contraseña = QLabel('Contraseña:')
        layout.addWidget(lbl_contraseña, 3, 0)
        self.txt_contraseña = QLineEdit()
        self.txt_contraseña.setEchoMode(QLineEdit.Password)
        layout.addWidget(self.txt_contraseña, 3, 1, 1, 2)

        # Género
        lbl_genero = QLabel('Género:')
        layout.addWidget(lbl_genero, 4, 0)
        self.radio_mas = QRadioButton('Masculino')
        self.radio_fem = QRadioButton('Femenino')
        layout.addWidget(self.radio_mas, 4, 1)
        layout.addWidget(self.radio_fem, 4, 2)
       
        #Botones de Radio  
        self.grupo_genero = QButtonGroup()
        self.grupo_genero.addButton(self.radio_mas)
        self.grupo_genero.addButton(self.radio_fem)

        # Selección de País
        lbl_pais = QLabel('País')
        layout.addWidget(lbl_pais, 5, 0)
        self.combo_pais = QComboBox()
        self.combo_pais.addItems(['Argentina', 'España', 'Alemania', 'Portugal', 'Brasil'])
        layout.addWidget(self.combo_pais, 5, 1, 1, 2)

        #Verificación de Términos y Condiciones 
        self.check_terminos = QCheckBox('Acepto los términos y condiciones')
        layout.addWidget(self.check_terminos, 6, 0, 1, 3)

        #Botón Registrarse
        btn_registrarse = QPushButton('Registrarse')
        btn_registrarse.clicked.connect(self.validar_formulario)
        layout.addWidget(btn_registrarse, 7, 0, 1, 3)

    def validar_formulario(self):
        nombre = self.txt_nombre.text().strip()
        email = self.txt_email.text().strip()
        password = self.txt_contraseña.text().strip()
         
        genero_seleccionado = self.grupo_genero.checkedButton()
        
        terminos = self.check_terminos.isChecked()

        if not nombre or not email or not password or genero_seleccionado is None or not terminos:
            QMessageBox.warning(self, 'Error', 'Por favor complete todos los campos y acepte los términos y condiciones.')
        else:
            pais = self.combo_pais.currentText()
            QMessageBox.information(self, 'Éxito', f'Registro exitoso para {nombre} de {pais}.')


if __name__ == '__main__':
    app = QApplication(sys.argv)
    ventana = Ventana()
    ventana.show()
    sys.exit(app.exec_())
