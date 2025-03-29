# semana-15
@@ -0,0 +1,20 @@
 import tkinter as tk
 from tkinter import messagebox
 
 def on_save_clicked():
     # Aquí se ejecutaría la lógica de guardar los datos
     # Por ejemplo, guardar los datos en un archivo o en una base de datos
     # Para este ejemplo, simplemente mostraremos un messagebox
     messagebox.showinfo("Guardar", "Los datos han sido guardados correctamente.")
 
 # Crear la ventana principal
 root = tk.Tk()
 root.title("Ejemplo de Escuchadores de Eventos")
 root.geometry("300x150")
 
 # Crear un botón y registrar el escuchador de eventos para el evento de clic
 save_button = tk.Button(root, text="Guardar", command=on_save_clicked)
 save_button.pack(pady=20)
 
 # Iniciar el bucle principal de la GUI
 root.mainloop()
@@ -0,0 +1,51 @@
 import tkinter as tk
 from tkinter import messagebox, scrolledtext
 
 
 class CommentApp:
     def __init__(self, master):
         self.master = master
         self.master.title('Sistema de Comentarios')
         self.master.geometry('500x250')
 
         # Etiqueta y campo de entrada para el nombre
         self.name_label = tk.Label(master, text='Nombre:')
         self.name_label.pack()
         self.name_entry = tk.Entry(master)
         self.name_entry.pack()
 
         # Etiqueta y campo de texto para el comentario
         self.comment_label = tk.Label(master, text='Comentario:')
         self.comment_label.pack()
         self.comment_text = scrolledtext.ScrolledText(master, height=5)
         self.comment_text.pack()
 
         # Botón para enviar el comentario
         self.submit_button = tk.Button(master, text='Enviar', command=self.submit_comment)
         self.submit_button.pack(pady=5)
 
         # Botón para limpiar los campos de entrada
         self.clear_button = tk.Button(master, text='Limpiar', command=self.clear_fields)
         self.clear_button.pack(pady=5)
 
     def submit_comment(self):
         # Recoge los valores de los campos de entrada
         name = self.name_entry.get()
         comment = self.comment_text.get("1.0", tk.END).strip()
 
         if name and comment:
             messagebox.showinfo("Comentario Enviado", f"Gracias {name}, tu comentario ha sido enviado.")
             self.clear_fields()
         else:
             messagebox.showwarning("Faltan Datos", "Por favor, completa todos los campos antes de enviar.")
 
     def clear_fields(self):
         # Limpia los campos de texto y área de texto
         self.name_entry.delete(0, tk.END)
         self.comment_text.delete('1.0', tk.END)
 
 
 if __name__ == '__main__':
     root = tk.Tk()
     app = CommentApp(root)

     @@ -0,0 +1,43 @@
 import tkinter as tk
 from tkinter import ttk, messagebox
 
 def on_enter_pressed_in_entry(event):
     # Agregar el texto del cuadro de entrada al Treeview
     text = text_entry.get()
     if text:
         treeview.insert('', tk.END, values=(text,))
         text_entry.delete(0, tk.END)
     else:
         messagebox.showwarning("Advertencia", "Por favor, ingresa texto antes de presionar Enter.")
 
 def on_escape_pressed(event):
     messagebox.showinfo("Evento de Tecla", "Tecla Escape presionada. Cerrando aplicación.")
     root.destroy()
 
 # Crear la ventana principal
 root = tk.Tk()
 root.title("Ejemplo Avanzado de Manejo de Eventos de Teclado")
 root.geometry("400x300")
 
 # Instrucciones
 instructions = tk.Label(root, text="Ingresa texto y presiona Enter para agregar al listado:\nPresiona Escape para cerrar la aplicación.",
                         justify=tk.CENTER, font=('Arial', 12))
 instructions.pack(pady=10)
 
 # Cuadro de entrada de texto
 text_entry = tk.Entry(root)
 text_entry.pack(pady=10)
 text_entry.focus()  # Poner el foco en el cuadro de entrada
 
 # Treeview para mostrar los textos agregados
 treeview = ttk.Treeview(root, columns=('Text'), show='headings')
 treeview.heading('Text', text='Textos Ingresados')
 treeview.pack(pady=10, fill=tk.BOTH, expand=True)
 
 # Vincular evento de tecla Enter solo al cuadro de texto
 text_entry.bind('<Return>', on_enter_pressed_in_entry)
 
 # Vincular evento de tecla Escape a la ventana principal
 root.bind('<Escape>', on_escape_pressed)
 
 root.mainloop()
 
     root.mainloop()
 
