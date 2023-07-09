from tkinter import *
import os
import sys
from tkinter import messagebox

#--VENTANA A
class Datos:
    def __init__(self):

        def validar_dni(*args):
            dni = self.obtenerDni.get()
            if len(dni) > 8:
                self.obtenerDni.set(dni[:8])

        def limitar_telefono(*args):
            telefono = self.obtenerTel.get()
            if len(telefono) > 9:
                self.obtenerTel.set(telefono[:9])

        def limitar_apellido(*args):
            apellido = self.obtenerApellido.get()
            if len(apellido) > 15:
                self.obtenerApellido.set(apellido[:15])

        def limitar_nombre(*args):
            nombre = self.obtenerNombre.get()
            if len(nombre) > 15:
                self.obtenerNombre.set(nombre[:15])

        def limitar_direccion(*args):
            direccion = self.obtenerDir.get()
            if len(direccion) > 38:
                self.obtenerDir.set(direccion[:38])

        def limpiar_datos():
            self.obtenerDni.set('')
            self.obtenerApellido.set('')
            self.obtenerNombre.set('')
            self.obtenerDir.set('')
            self.obtenerTel.set('')
            
        def salir():
            sys.exit()
        
        self.root=Tk()
        
        self.titulo = Label(self.root, text='- S O D I M A C -', font=('Times New Roman', 24, 'bold'), foreground='DodgerBlue4', background='skyBlue1')
        self.titulo.pack(pady=13)
        
        self.root.title('Datos del cliente')
        self.root.geometry("500x250")
        self.root.resizable(False, False)
        self.root.configure(background='skyBlue1')
        
        self.principal = Frame(self.root)
        self.principal.pack()
        self.principal.configure(background='skyBlue1')
        
        #--DNI
        self.obtenerDni = StringVar()
        self.lDni = Label(self.principal, text='DNI:', background='skyBlue1')
        self.lDni.grid(row=1, column=0, sticky='e', pady=5, padx=5)
        self.tDni = Entry(self.principal, textvariable=self.obtenerDni, justify="center", background='azure')
        self.tDni.grid(row=1, column=1, pady=5, padx=5)

        self.obtenerDni.trace('w', validar_dni)
        
        #--APELLIDO
        self.obtenerApellido = StringVar()
        self.lApellido = Label(self.principal, text='Apellido:', background='skyBlue1')
        self.lApellido.grid(row=2, column=0, sticky='e', pady=5, padx=5)
        self.tApellido = Entry(self.principal, textvariable=self.obtenerApellido, background='azure')
        self.tApellido.grid(row=2, column=1, pady=5, padx=5)

        self.obtenerApellido.trace('w', limitar_apellido)

        #--NOMBRE
        self.obtenerNombre = StringVar()
        self.lNombre = Label(self.principal, text='Nombre:', background='skyBlue1')
        self.lNombre.grid(row=2, column=2, sticky='e', pady=5, padx=5)
        self.tNombre = Entry(self.principal, textvariable=self.obtenerNombre, background='azure')
        self.tNombre.grid(row=2, column=3, pady=5, padx=5)

        self.obtenerNombre.trace('w', limitar_nombre)

        #--DIRECCION
        self.obtenerDir = StringVar()
        self.lDireccion = Label(self.principal, text='Dirección:', background='skyBlue1')
        self.lDireccion.grid(row=3, column=0, sticky='e', pady=5, padx=5)
        self.tDireccion = Entry(self.principal, textvariable=self.obtenerDir, background='azure')
        self.tDireccion.grid(row=3, column=1, columnspan=3, sticky='we', pady=5, padx=5)

        self.obtenerDir.trace('w', limitar_direccion)

        #TELEFONO
        self.obtenerTel = StringVar()
        self.lTel = Label(self.principal, text='Teléfono:', background='skyBlue1')
        self.lTel.grid(row=4, column=0, sticky='e', pady=5, padx=5)
        self.tTel = Entry(self.principal, textvariable=self.obtenerTel, background='azure')
        self.tTel.grid(row=4, column=1, columnspan=3, sticky='we', pady=5, padx=5)

        self.obtenerTel.trace('w', limitar_telefono)
        
        self.bntSiguiente = Frame(self.root)
        self.bntSiguiente.pack()
        self.bntSiguiente.configure(background='skyBlue1')
        
        #--SIGUIENTE
        def advertencia():
            if self.obtenerDni.get() == '' or self.obtenerApellido.get() == '' or self.obtenerNombre.get() == '' or self.obtenerDir.get() == '' or self.obtenerTel.get() == '':
                messagebox.showwarning('Advertencia', 'Debe ingresar los datos requeridos.')
            else:
                self.abrirProductos()
        
        siguiente = Button(self.bntSiguiente, text='Siguiente', background='DodgerBlue3', foreground='azure', command=advertencia)
        siguiente.grid(row=5, column=3, pady=12, padx=5)
        
        #--LIMPIAR
        limpiar = Button(self.bntSiguiente, text='Limpiar', background='DodgerBlue3', foreground='azure', command=limpiar_datos)
        limpiar.grid(row=5, column=4, pady=8, padx=5)

        #--SALIR
        salir = Button(self.bntSiguiente, text='Salir', background='DodgerBlue3', foreground='azure', command=salir)
        salir.grid(row=5, column=5, pady=8, padx=5)
        
        self.root.mainloop()
        
    def abrirProductos(self):
        dni=self.obtenerDni.get()
        apellido=self.obtenerApellido.get()
        nombre=self.obtenerNombre.get()
        direccion=self.obtenerDir.get()
        telefono=self.obtenerTel.get()
        self.root.destroy()
        Productos(dni, apellido, nombre, direccion, telefono)

#--VENTANA B
class Productos:
    def __init__(self, dni, apellido, nombre, direccion, telefono):
        
        def limpiar():
            self.tCodigo1.delete(0, END)
            self.tDes1.configure(state="normal")
            self.tDes1.delete(0, END)
            self.tDes1.configure(state="readonly")
            self.tCantidad1.delete(0, END)
            self.tPrecio1.configure(state="normal")
            self.tPrecio1.delete(0, END)
            self.tPrecio1.configure(state="readonly")
            
            self.tCodigo2.delete(0, END)
            self.tDes2.configure(state="normal")
            self.tDes2.delete(0, END)
            self.tDes2.configure(state="readonly")
            self.tCantidad2.delete(0, END)
            self.tPrecio2.configure(state="normal")
            self.tPrecio2.delete(0, END)
            self.tPrecio2.configure(state="readonly")
            
            self.tCodigo3.delete(0, END)
            self.tDes3.configure(state="normal")
            self.tDes3.delete(0, END)
            self.tDes3.configure(state="readonly")
            self.tCantidad3.delete(0, END)
            self.tPrecio3.configure(state="normal")
            self.tPrecio3.delete(0, END)
            self.tPrecio3.configure(state="readonly")
            
            self.tCodigo4.delete(0, END)
            self.tDes4.configure(state="normal")
            self.tDes4.delete(0, END)
            self.tDes4.configure(state="readonly")
            self.tCantidad4.delete(0, END)
            self.tPrecio4.configure(state="normal")
            self.tPrecio4.delete(0, END)
            self.tPrecio4.configure(state="readonly")
        
        self.root = Tk()

        self.titulo1 = Label(self.root, text='- P R O D U C T O S -', font=('Times New Roman', 20, 'bold'), background='skyBlue1', foreground='DodgerBlue4')
        self.titulo1.pack(pady=15)

        self.root.title('Productos')
        self.root.geometry("500x550")
        self.root.resizable(False, False)
        self.root.configure(background='skyBlue1')
        
        self.titulo1 = Label(self.root, text='=========================================', font=('Times New Roman', 15, 'bold'), background='skyBlue1', foreground='DodgerBlue4')
        self.titulo1.pack(pady=1)

        self.productos = Frame(self.root)
        self.productos.pack()
        self.productos.configure(background='skyBlue1')

        self.titulo1 = Label(self.root, text='=========================================', font=('Times New Roman', 15, 'bold'), background='skyBlue1', foreground='DodgerBlue4')
        self.titulo1.pack(pady=9)
        
        #--PRODUCTOS
        Label(self.productos, text='|    Código    |', background='skyBlue1').grid(row=0, column=0, pady=5, padx=20)
        Label(self.productos, text='|            Descripción            |', background='skyBlue1').grid(row=0, column=1, pady=5, padx=20)
        Label(self.productos, text='|    Precio    |', background='skyBlue1').grid(row=0, column=2, pady=5, padx=20)

        Label(self.productos, text='001', background='skyBlue1').grid(row=1, column=0)
        Label(self.productos, text='Clavos (1kg)', background='skyBlue1').grid(row=1, column=1)
        Label(self.productos, text='S/5.00', background='skyBlue1').grid(row=1, column=2)

        Label(self.productos, text='002', background='skyBlue1').grid(row=2, column=0)
        Label(self.productos, text='Martillo (1pz)', background='skyBlue1').grid(row=2, column=1)
        Label(self.productos, text='S/9.00', background='skyBlue1').grid(row=2, column=2)

        Label(self.productos, text='003', background='skyBlue1').grid(row=3, column=0)
        Label(self.productos, text='Focos LED (1pz)', background='skyBlue1').grid(row=3, column=1)
        Label(self.productos, text='S/12.00', background='skyBlue1').grid(row=3, column=2)

        Label(self.productos, text='004', background='skyBlue1').grid(row=4, column=0)
        Label(self.productos, text='Taladro 10mm (1pz)', background='skyBlue1').grid(row=4, column=1)
        Label(self.productos, text='S/149.00', background='skyBlue1').grid(row=4, column=2)

        Label(self.productos, text='005', background='skyBlue1').grid(row=5, column=0)
        Label(self.productos, text='Cinta (25mm x 10m)', background='skyBlue1').grid(row=5, column=1)
        Label(self.productos, text='S/3.00', background='skyBlue1').grid(row=5, column=2)

        self.boleta = Frame(self.root)
        self.boleta.pack()
        self.boleta.configure(background='skyBlue1')
        
        #--CODIGO
        def actualizar_descripcion(event):
            codigo = self.tCodigo1.get()
            if codigo == '001':
                self.tDes1.configure(state="normal")
                self.tDes1.delete(0, END)
                self.tDes1.insert(0, 'Clavos 1kg')
                self.tDes1.configure(state="readonly")
            elif codigo == '002':
                self.tDes1.configure(state="normal")
                self.tDes1.delete(0, END)
                self.tDes1.insert(0, 'Martillo 1pz')
                self.tDes1.configure(state="readonly")
            elif codigo == '003':
                self.tDes1.configure(state="normal")
                self.tDes1.delete(0, END)
                self.tDes1.insert(0, 'Focos LED 1pz')
                self.tDes1.configure(state="readonly")
            elif codigo == '004':
                self.tDes1.configure(state="normal")
                self.tDes1.delete(0, END)
                self.tDes1.insert(0, 'Taladro 10mm (1pz)')
                self.tDes1.configure(state="readonly")
            elif codigo == '005':
                self.tDes1.configure(state="normal")
                self.tDes1.delete(0, END)
                self.tDes1.insert(0, 'Cinta (25mm x 10m)')
                self.tDes1.configure(state="readonly") 
                
        def actualizar_descripcion2(event):
            codigo2 = self.tCodigo2.get()
            if codigo2 == '001':
                self.tDes2.configure(state="normal")
                self.tDes2.delete(0, END)
                self.tDes2.insert(0, 'Clavos 1kg')
                self.tDes2.configure(state="readonly")
            elif codigo2 == '002':
                self.tDes2.configure(state="normal")
                self.tDes2.delete(0, END)
                self.tDes2.insert(0, 'Martillo 1pz')
                self.tDes2.configure(state="readonly")
            elif codigo2 == '003':
                self.tDes2.configure(state="normal")
                self.tDes2.delete(0, END)
                self.tDes2.insert(0, 'Focos LED 1pz')
                self.tDes2.configure(state="readonly")
            elif codigo2 == '004':
                self.tDes2.configure(state="normal")
                self.tDes2.delete(0, END)
                self.tDes2.insert(0, 'Taladro 10mm (1pz)')
                self.tDes2.configure(state="readonly")
            elif codigo2 == '005':
                self.tDes2.configure(state="normal")
                self.tDes2.delete(0, END)
                self.tDes2.insert(0, 'Cinta (25mm x 10m)')
                self.tDes2.configure(state="readonly")
                
        def actualizar_descripcion4(event):
            codigo4 = self.tCodigo3.get()
            if codigo4 == '001':
                self.tDes3.configure(state="normal")
                self.tDes3.delete(0, END)
                self.tDes3.insert(0, 'Clavos 1kg')
                self.tDes3.configure(state="readonly")
            elif codigo4 == '002':
                self.tDes3.configure(state="normal")
                self.tDes3.delete(0, END)
                self.tDes3.insert(0, 'Martillo 1pz')
                self.tDes3.configure(state="readonly")
            elif codigo4 == '003':
                self.tDes3.configure(state="normal")
                self.tDes3.delete(0, END)
                self.tDes3.insert(0, 'Focos LED 1pz')
                self.tDes3.configure(state="readonly")
            elif codigo4 == '004':
                self.tDes3.configure(state="normal")
                self.tDes3.delete(0, END)
                self.tDes3.insert(0, 'Taladro 10mm (1pz)')
                self.tDes3.configure(state="readonly")
            elif codigo4 == '005':
                self.tDes3.configure(state="normal")
                self.tDes3.delete(0, END)
                self.tDes3.insert(0, 'Cinta (25mm x 10m)')
                self.tDes3.configure(state="readonly")

        def actualizar_descripcion5(event):
            codigo5 = self.tCodigo4.get()
            if codigo5 == '001':
                self.tDes4.configure(state="normal")
                self.tDes4.delete(0, END)
                self.tDes4.insert(0, 'Clavos 1kg')
                self.tDes4.configure(state="readonly")
            elif codigo5 == '002':
                self.tDes4.configure(state="normal")
                self.tDes4.delete(0, END)
                self.tDes4.insert(0, 'Martillo 1pz')
                self.tDes4.configure(state="readonly")
            elif codigo5 == '003':
                self.tDes4.configure(state="normal")
                self.tDes4.delete(0, END)
                self.tDes4.insert(0, 'Focos LED 1pz')
                self.tDes4.configure(state="readonly")
            elif codigo5 == '004':
                self.tDes4.configure(state="normal")
                self.tDes4.delete(0, END)
                self.tDes4.insert(0, 'Taladro 10mm (1pz)')
                self.tDes4.configure(state="readonly")
            elif codigo5 == '005':
                self.tDes4.configure(state="normal")
                self.tDes4.delete(0, END)
                self.tDes4.insert(0, 'Cinta (25mm x 10m)')
                self.tDes4.configure(state="readonly")

        self.lCodigo = Label(self.boleta, text='Código', background='skyBlue1')
        self.lCodigo.grid(row=4, column=0, sticky='e', pady=5, padx=25)
        self.tCodigo1 = Entry(self.boleta, width=7, justify="center", background='azure')
        self.tCodigo1.grid(row=5, column=0, pady=5, padx=25)
        self.tCodigo1.bind('<FocusOut>', actualizar_descripcion)

        self.tCodigo2 = Entry(self.boleta, width=7, justify="center", background='azure')
        self.tCodigo2.grid(row=6, column=0, pady=5, padx=25)
        self.tCodigo2.bind('<FocusOut>', actualizar_descripcion2)

        self.tCodigo3 = Entry(self.boleta, width=7, justify="center", background='azure')
        self.tCodigo3.grid(row=7, column=0, pady=5, padx=25)
        self.tCodigo3.bind('<FocusOut>', actualizar_descripcion4)

        self.tCodigo4 = Entry(self.boleta, width=7, justify="center", background='azure')
        self.tCodigo4.grid(row=8, column=0, pady=5, padx=25)
        self.tCodigo4.bind('<FocusOut>', actualizar_descripcion5)
        
        #--DESCRIPCION
        self.lDes = Label(self.boleta, text='Descripción', background='skyBlue1')
        self.lDes.grid(row=4, column=1, sticky='ew', pady=5, padx=25)
        self.tDes1 = Entry(self.boleta, width=20, state="readonly", justify="center")
        self.tDes1.grid(row=5, column=1, pady=5, padx=25)
        self.tDes2 = Entry(self.boleta, width=20, state="readonly", justify="center")
        self.tDes2.grid(row=6, column=1, pady=5, padx=25)
        self.tDes3 = Entry(self.boleta, width=20, state="readonly", justify="center")
        self.tDes3.grid(row=7, column=1, pady=5, padx=25)
        self.tDes4 = Entry(self.boleta, width=20, state="readonly", justify="center")
        self.tDes4.grid(row=8, column=1, pady=5, padx=25)
        
        #--CANTIDAD
        def actualizar_precio(event):
            cantidad1 = int(self.tCantidad1.get())
            codigo = self.tCodigo1.get()
            if codigo == '001':
                precio = 5.00 * cantidad1
                self.tPrecio1.configure(state="normal")
                self.tPrecio1.delete(0, END)
                self.tPrecio1.insert(0, precio)
                self.tPrecio1.configure(state="readonly")
            elif codigo == '002':
                precio = 9.00 * cantidad1
                self.tPrecio1.configure(state="normal")
                self.tPrecio1.delete(0, END)
                self.tPrecio1.insert(0, precio)
                self.tPrecio1.configure(state="readonly")
            elif codigo == '003':
                precio = 12.00 * cantidad1
                self.tPrecio1.configure(state="normal")
                self.tPrecio1.delete(0, END)
                self.tPrecio1.insert(0, precio)
                self.tPrecio1.configure(state="readonly")
            elif codigo == '004':
                precio = 149.00 * cantidad1
                self.tPrecio1.configure(state="normal")
                self.tPrecio1.delete(0, END)
                self.tPrecio1.insert(0, precio)
                self.tPrecio1.configure(state="readonly")
            elif codigo == '005':
                precio = 3.00 * cantidad1
                self.tPrecio1.configure(state="normal")
                self.tPrecio1.delete(0, END)
                self.tPrecio1.insert(0, precio)
                self.tPrecio1.configure(state="readonly")
            else:
                self.tPrecio1.configure(state="normal")
                self.tPrecio1.delete(0, END)
                self.tPrecio1.configure(state="readonly")
                
        def actualizar_precio2(event):
            cantidad2 = int(self.tCantidad2.get())
            codigo2 = self.tCodigo2.get()
            if codigo2 == '001':
                precio2 = 5.00 * cantidad2
                self.tPrecio2.configure(state="normal")
                self.tPrecio2.delete(0, END)
                self.tPrecio2.insert(0, precio2)
                self.tPrecio2.configure(state="readonly")
            elif codigo2 == '002':
                precio2 = 9.00 * cantidad2
                self.tPrecio2.configure(state="normal")
                self.tPrecio2.delete(0, END)
                self.tPrecio2.insert(0, precio2)
                self.tPrecio2.configure(state="readonly")
            elif codigo2 == '003':
                precio2 = 12.00 * cantidad2
                self.tPrecio2.configure(state="normal")
                self.tPrecio2.delete(0, END)
                self.tPrecio2.insert(0, precio2)
                self.tPrecio2.configure(state="readonly")
            elif codigo2 == '004':
                precio2 = 149.00 * cantidad2
                self.tPrecio2.configure(state="normal")
                self.tPrecio2.delete(0, END)
                self.tPrecio2.insert(0, precio2)
                self.tPrecio2.configure(state="readonly")
            elif codigo2 == '005':
                precio2 = 3.00 * cantidad2
                self.tPrecio2.configure(state="normal")
                self.tPrecio2.delete(0, END)
                self.tPrecio2.insert(0, precio2)
                self.tPrecio2.configure(state="readonly")
            else:
                self.tPrecio2.configure(state="normal")
                self.tPrecio2.delete(0, END)
                self.tPrecio2.configure(state="readonly")

        def actualizar_precio4(event):
            cantidad4 = int(self.tCantidad3.get())
            codigo4 = self.tCodigo3.get()
            if codigo4 == '001':
                precio4 = 5.00 * cantidad4
                self.tPrecio3.configure(state="normal")
                self.tPrecio3.delete(0, END)
                self.tPrecio3.insert(0, precio4)
                self.tPrecio3.configure(state="readonly")
            elif codigo4 == '002':
                precio4 = 9.00 * cantidad4
                self.tPrecio3.configure(state="normal")
                self.tPrecio3.delete(0, END)
                self.tPrecio3.insert(0, precio4)
                self.tPrecio3.configure(state="readonly")
            elif codigo4 == '003':
                precio4 = 12.00 * cantidad4
                self.tPrecio3.configure(state="normal")
                self.tPrecio3.delete(0, END)
                self.tPrecio3.insert(0, precio4)
                self.tPrecio3.configure(state="readonly")
            elif codigo4 == '004':
                precio4 = 149.00 * cantidad4
                self.tPrecio3.configure(state="normal")
                self.tPrecio3.delete(0, END)
                self.tPrecio3.insert(0, precio4)
                self.tPrecio3.configure(state="readonly")
            elif codigo4 == '005':
                precio4 = 3.00 * cantidad4
                self.tPrecio3.configure(state="normal")
                self.tPrecio3.delete(0, END)
                self.tPrecio3.insert(0, precio4)
                self.tPrecio3.configure(state="readonly")
            else:
                self.tPrecio3.configure(state="normal")
                self.tPrecio3.delete(0, END)
                self.tPrecio3.configure(state="readonly")

        def actualizar_precio5(event):
            cantidad5 = int(self.tCantidad4.get())
            codigo5 = self.tCodigo4.get()
            if codigo5 == '001':
                precio5 = 5.00 * cantidad5
                self.tPrecio4.configure(state="normal")
                self.tPrecio4.delete(0, END)
                self.tPrecio4.insert(0, precio5)
                self.tPrecio4.configure(state="readonly")
            elif codigo5 == '002':
                precio5 = 9.00 * cantidad5
                self.tPrecio4.configure(state="normal")
                self.tPrecio4.delete(0, END)
                self.tPrecio4.insert(0, precio5)
                self.tPrecio4.configure(state="readonly")
            elif codigo5 == '003':
                precio5 = 12.00 * cantidad5
                self.tPrecio4.configure(state="normal")
                self.tPrecio4.delete(0, END)
                self.tPrecio4.insert(0, precio5)
                self.tPrecio4.configure(state="readonly")
            elif codigo5 == '004':
                precio5 = 149.00 * cantidad5
                self.tPrecio4.configure(state="normal")
                self.tPrecio4.delete(0, END)
                self.tPrecio4.insert(0, precio5)
                self.tPrecio4.configure(state="readonly")
            elif codigo5 == '005':
                precio5 = 3.00 * cantidad5
                self.tPrecio4.configure(state="normal")
                self.tPrecio4.delete(0, END)
                self.tPrecio4.insert(0, precio5)
                self.tPrecio4.configure(state="readonly")
            else:
                self.tPrecio4.configure(state="normal")
                self.tPrecio4.delete(0, END)
                self.tPrecio4.configure(state="readonly")

        self.lCantidad = Label(self.boleta, text='Cantidad', background='skyBlue1')
        self.lCantidad.grid(row=4, column=3, sticky='ew', pady=5, padx=25)
        self.tCantidad1 = Entry(self.boleta, width=7, justify="center", background='azure')
        self.tCantidad1.grid(row=5, column=3, pady=5, padx=25)
        self.tCantidad1.bind("<FocusOut>", actualizar_precio)

        self.tCantidad2 = Entry(self.boleta, width=7, justify="center", background='azure')
        self.tCantidad2.grid(row=6, column=3, pady=5, padx=25)
        self.tCantidad2.bind("<FocusOut>", actualizar_precio2)

        self.tCantidad3 = Entry(self.boleta, width=7, justify="center", background='azure')
        self.tCantidad3.grid(row=7, column=3, pady=5, padx=25)
        self.tCantidad3.bind("<FocusOut>", actualizar_precio4)

        self.tCantidad4 = Entry(self.boleta, width=7, justify="center", background='azure')
        self.tCantidad4.grid(row=8, column=3, pady=5, padx=25)
        self.tCantidad4.bind("<FocusOut>", actualizar_precio5)
        
        #--PRECIO
        self.lPrecio = Label(self.boleta, text='Precio', background='skyBlue1')
        self.lPrecio.grid(row=4, column=4, sticky='ew', pady=5, padx=25)
        self.tPrecio1 = Entry(self.boleta, width=10, state="readonly", justify="center", background='azure')
        self.tPrecio1.grid(row=5, column=4, pady=5, padx=25)
        self.tPrecio2 = Entry(self.boleta, width=10, state="readonly", justify="center", background='azure')
        self.tPrecio2.grid(row=6, column=4, pady=5, padx=25)
        self.tPrecio3 = Entry(self.boleta, width=10, state="readonly", justify="center", background='azure')
        self.tPrecio3.grid(row=7, column=4, pady=5, padx=25)
        self.tPrecio4 = Entry(self.boleta, width=10, state="readonly", justify="center", background='azure')
        self.tPrecio4.grid(row=8, column=4, pady=5, padx=25)
            
        #--TOTAL
        def calcular_total():
            total = 0
            precios = [self.tPrecio1.get(), self.tPrecio2.get(), self.tPrecio3.get(), self.tPrecio4.get()]
            
            for precio in precios:
                try:
                    total += float(precio)
                except ValueError:
                    pass
            
            self.lTotal.configure(state="normal")
            self.lTotal.delete(0, END)
            self.lTotal.insert(0, total)
            self.lTotal.configure(state="readonly")

        self.lTotal = Label(self.boleta, text='Precio Total', background='skyBlue1')
        self.lTotal.grid(row=10, column=3, sticky='ew', pady=25, padx=25)
        self.lTotal = Entry(self.boleta, width=10, state="readonly", justify="center")
        self.lTotal.grid(row=10, column=4, pady=5, padx=25)

        self.Bole = Frame(self.root)
        self.Bole.pack()
        self.Bole.configure(background='skyBlue1')
        
        #--PAGO
        def advertencia1():
            if self.tCodigo1.get() == '' or self.tCodigo2.get() == '' or self.tCodigo3.get() == '' or self.tCodigo4.get() == '' or self.tCantidad1.get() == '' or self.tCantidad2.get() == '' or self.tCantidad3.get() == '' or self.tCantidad4.get() == '':
                messagebox.showwarning('Advertencia', 'Ingresa los productos que desea comprar')
            else:
                self.abrirBoleta(dni, apellido, nombre, direccion, telefono)

        siguiente = Button(self.Bole, text='Confirmar pago', background='DodgerBlue3', foreground='azure', command=advertencia1)
        siguiente.grid(row=5, column=3, pady=0, padx=5)

        #--TOTAL
        botonCalcularTotal = Button(self.Bole, text="Calcular Total", background='DodgerBlue3', foreground='azure', command=calcular_total)
        botonCalcularTotal.grid(row=5, column=2, pady=0, padx=5)

        #--LIMPIAR
        limpiar = Button(self.Bole, text='Limpiar', background='DodgerBlue3', foreground='azure', command=limpiar)
        limpiar.grid(row=5, column=4, pady=0, padx=5)
        
        self.root.mainloop()
        
    def abrirBoleta(self, dni, apellido, nombre, direccion, telefono):
        codigo1=self.tCodigo1.get()
        codigo2=self.tCodigo2.get()
        codigo3=self.tCodigo3.get()
        codigo4=self.tCodigo4.get()
        
        descripcion1=self.tDes1.get()
        descripcion2=self.tDes2.get()
        descripcion3=self.tDes3.get()
        descripcion4=self.tDes4.get()
        
        cantidad1=self.tCantidad1.get()
        cantidad2=self.tCantidad2.get()
        cantidad3=self.tCantidad3.get()
        cantidad4=self.tCantidad4.get()
        
        precio1=self.tPrecio1.get()
        precio2=self.tPrecio2.get()
        precio3=self.tPrecio3.get()
        precio4=self.tPrecio4.get()
        
        total=self.lTotal.get()
        
        self.root.destroy()
        BoletaGen(dni, apellido, nombre, direccion, telefono, codigo1, codigo2, codigo3, codigo4, descripcion1, descripcion2, descripcion3, descripcion4, cantidad1, cantidad2, cantidad3, cantidad4, precio1, precio2, precio3, precio4, total)

#--VENTANA C
class BoletaGen:
        def __init__(self, dni, apellido, nombre, direccion, telefono, codigo1, codigo2, codigo3, codigo4, descripcion1, descripcion2, descripcion3, descripcion4, cantidad1, cantidad2, cantidad3, cantidad4, precio1, precio2, precio3, precio4, total):
            
            def finalizar_pago():
                messagebox.showinfo("Confirmación", "Pago exitoso! ¡Gracias por su compra!")
                self.root.destroy()

            def cancelar_compra():
                respuesta = messagebox.askyesno("Confirmación", "¿Desea cancelar esta compra?")
                if respuesta:
                    messagebox.showwarning("Advertencia", "Compra cancelada")
                    self.root.destroy()

            self.root = Tk()

            self.titulo4 = Label(self.root, text='- Boleta Electrónica -', font=('Times New Roman', 24, 'bold'), foreground='DodgerBlue4', background='skyBlue1')
            self.titulo4.pack(pady=15)

            self.titulo5 = Label(self.root, text='=========================================', font=('Times New Roman', 15, 'bold'), background='skyBlue1')
            self.titulo5.pack(pady=1)

            self.root.title('Boleta')
            self.root.geometry("500x556")
            self.root.resizable(False, False)
            self.root.configure(background='skyBlue1')

            self.facto = Frame(self.root)
            self.facto.pack()
            self.facto.configure(background='skyBlue1')

            #--DNI
            self.dni21=StringVar(value=dni)
            self.lDni = Label(self.facto, text='DNI:', background='skyBlue1')
            self.lDni.grid(row=1, column=0, sticky='ew', pady=5, padx=5)
            self.tDni = Entry(self.facto, textvariable=self.dni21, state="readonly", justify="center")
            self.tDni.grid(row=1, column=1, pady=5, padx=5)

            #--APELLIDO
            self.ape21=StringVar(value=apellido)
            self.lApellido = Label(self.facto, text='Apellido:', background='skyBlue1')
            self.lApellido.grid(row=2, column=0, sticky='e', pady=5, padx=5)
            self.tApellido = Entry(self.facto, textvariable=self.ape21, state="readonly", justify="center")
            self.tApellido.grid(row=2, column=1, pady=5, padx=5)

            #--NOMBRE
            self.nombre21=StringVar(value=nombre)
            self.lNombre = Label(self.facto, text='Nombre:', background='skyBlue1')
            self.lNombre.grid(row=2, column=2, sticky='e', pady=5, padx=5)
            self.tNombre = Entry(self.facto, textvariable=self.nombre21, state="readonly", justify="center")
            self.tNombre.grid(row=2, column=3, pady=5, padx=5)

            #--DIRECCION
            self.direcc21=StringVar(value=direccion)
            self.lDireccion = Label(self.facto, text='Dirección:', background='skyBlue1')
            self.lDireccion.grid(row=3, column=0, sticky='e', pady=5, padx=5)
            self.tDireccion = Entry(self.facto, textvariable=self.direcc21, state="readonly", justify="center")
            self.tDireccion.grid(row=3, column=1, columnspan=3, sticky='we', pady=5, padx=5)

            #TELEFONO
            self.tele21=StringVar(value=telefono)
            self.lTel = Label(self.facto, text='Teléfono:', background='skyBlue1')
            self.lTel.grid(row=4, column=0, sticky='e', pady=5, padx=5)
            self.tTel = Entry(self.facto, textvariable=self.tele21, state="readonly", justify="center")
            self.tTel.grid(row=4, column=1, columnspan=3, sticky='we', pady=5, padx=5)

            self.titulo6 = Label(self.root, text='=========================================', font=('Times New Roman', 15, 'bold'), background='skyBlue1')
            self.titulo6.pack(pady=1)

            self.facturaProd = Frame(self.root)
            self.facturaProd.pack()
            self.facturaProd.configure(background='skyBlue1')

            #--CODIGO
            self.code1=StringVar(value=codigo1)
            self.lCodigo = Label(self.facturaProd, text='Código', background='skyBlue1')
            self.lCodigo.grid(row=5, column=0, sticky='e', pady=5, padx=25)
            self.tCodigo1 = Entry(self.facturaProd, textvariable=self.code1,  width=7, state="readonly", justify="center")
            self.tCodigo1.grid(row=6, column=0, pady=5, padx=25)

            self.code2=StringVar(value=codigo2)
            self.tCodigo2 = Entry(self.facturaProd, textvariable=self.code2, width=7, state="readonly", justify="center")
            self.tCodigo2.grid(row=7, column=0, pady=5, padx=25)
            
            self.code3=StringVar(value=codigo3)
            self.tCodigo3 = Entry(self.facturaProd, textvariable=self.code3, width=7, state="readonly", justify="center")
            self.tCodigo3.grid(row=8, column=0, pady=5, padx=25)
            
            self.code4=StringVar(value=codigo4)
            self.tCodigo4 = Entry(self.facturaProd, textvariable=self.code4, width=7, state="readonly", justify="center")
            self.tCodigo4.grid(row=9, column=0, pady=5, padx=25)

            #--DESCRIPCION
            self.decr1=StringVar(value=descripcion1)
            self.lDes = Label(self.facturaProd, text='Descripción', background='skyBlue1')
            self.lDes.grid(row=5, column=1, sticky='ew', pady=5, padx=25)
            self.tDes1 = Entry(self.facturaProd, textvariable=self.decr1, width=20, state="readonly", justify="center")
            self.tDes1.grid(row=6, column=1, pady=5, padx=25)

            self.decr2=StringVar(value=descripcion2)
            self.tDes2 = Entry(self.facturaProd, textvariable=self.decr2, width=20, state="readonly", justify="center")
            self.tDes2.grid(row=7, column=1, pady=5, padx=25)
            
            self.decr3=StringVar(value=descripcion3)
            self.tDes3 = Entry(self.facturaProd, textvariable=self.decr3, width=20, state="readonly", justify="center")
            self.tDes3.grid(row=8, column=1, pady=5, padx=25)
            
            self.decr4=StringVar(value=descripcion4)
            self.tDes4 = Entry(self.facturaProd, textvariable=self.decr4, width=20, state="readonly", justify="center")
            self.tDes4.grid(row=9, column=1, pady=5, padx=25)
            
            #--CANTIDAD
            self.can1=StringVar(value=cantidad1)
            self.lCantidad = Label(self.facturaProd, text='Cantidad', background='skyBlue1')
            self.lCantidad.grid(row=5, column=3, sticky='ew', pady=5, padx=25)
            self.tCantidad1 = Entry(self.facturaProd, textvariable=self.can1, width=7, state="readonly", justify="center")
            self.tCantidad1.grid(row=6, column=3, pady=5, padx=25)

            self.can2=StringVar(value=cantidad2)
            self.tCantidad2 = Entry(self.facturaProd, textvariable=self.can2, width=7, state="readonly", justify="center")
            self.tCantidad2.grid(row=7, column=3, pady=5, padx=25)
            
            self.can3=StringVar(value=cantidad3)
            self.tCantidad3 = Entry(self.facturaProd, textvariable=self.can3, width=7, state="readonly", justify="center")
            self.tCantidad3.grid(row=8, column=3, pady=5, padx=25)
            
            self.can4=StringVar(value=cantidad4)
            self.tCantidad4 = Entry(self.facturaProd, textvariable=self.can4, width=7, state="readonly", justify="center")
            self.tCantidad4.grid(row=9, column=3, pady=5, padx=25)

            #--PRECIO
            self.pre1=StringVar(value=precio1)
            self.lPrecio = Label(self.facturaProd, text='Precio', background='skyBlue1')
            self.lPrecio.grid(row=5, column=4, sticky='ew', pady=5, padx=25)
            self.tPrecio1 = Entry(self.facturaProd, textvariable=self.pre1, width=7, state="readonly", justify="center")
            self.tPrecio1.grid(row=6, column=4, pady=5, padx=25)

            self.pre2=StringVar(value=precio2)
            self.tPrecio2 = Entry(self.facturaProd, textvariable=self.pre2, width=7, state="readonly", justify="center")
            self.tPrecio2.grid(row=7, column=4, pady=5, padx=25)
            
            self.pre3=StringVar(value=precio3)
            self.tPrecio3 = Entry(self.facturaProd, textvariable=self.pre3, width=7, state="readonly", justify="center")
            self.tPrecio3.grid(row=8, column=4, pady=5, padx=25)
            
            self.pre4=StringVar(value=precio4)
            self.tPrecio4 = Entry(self.facturaProd, textvariable=self.pre4, width=7, state="readonly", justify="center")
            self.tPrecio4.grid(row=9, column=4, pady=5, padx=25)
            
            #--TOTAL
            self.toto=StringVar(value=total)
            self.lTotal = Label(self.facturaProd, text='Precio Total', background='skyBlue1')
            self.lTotal.grid(row=10, column=3, sticky='ew', pady=25, padx=25)
            self.lTotal = Entry(self.facturaProd, textvariable=self.toto, width=7, state="readonly", justify="center")
            self.lTotal.grid(row=10, column=4, pady=5, padx=25)

            self.titulo6 = Label(self.root, text='=========================================', font=('Times New Roman', 15, 'bold'), background='skyBlue1')
            self.titulo6.pack(pady=0)

            self.facturaSe = Frame(self.root)
            self.facturaSe.pack()
            self.facturaSe.configure(background='skyBlue1')

            #--PAGAR
            self.btnFinalizarPago = Button(self.facturaSe, text="Finalizar pago", background='DodgerBlue3', foreground='azure', command=finalizar_pago)
            self.btnFinalizarPago.grid(row=11, column=3, pady=5, padx=25)

            #--CANCELAR
            self.btnCancelarCompra = Button(self.facturaSe, text="Cancelar compra", background='DodgerBlue3', foreground='azure', command=cancelar_compra)
            self.btnCancelarCompra.grid(row=11, column=4, pady=5, padx=25)
            
            self.root.mainloop()
            
ventana_a = Datos()