# METODOS_DLL_ANTHONY_RODRIGUEZ_014_25_27
Buen día, este es mi repositorio sobre la tarea relacionada a los metodos de dll (Double Linked List), misma que fue asignada el día 12/03/2026 en el laboratorio de cómputo.

A continuación presento mi código:

#LISTAS DOBLEMENTE ENLAZADAS
class Nodo:
    def __init__(self, tipo_dato=None, next=None, tail=None):
        self.tipo_dato = tipo_dato
        self.next = next
        self.tail = tail

    def __str__(self):
        return (self.tipo_dato)   


class Mi_lista_doble:
    def __init__(self):
        self.cabeza = None
        self.cola = None
        self.contador = 0

#INSERTARLE DATOS A LA LISTA
    def insertar(self, tipo_dato):
        nodo = Nodo(tipo_dato)      
        if self.cabeza is None:
            self.cabeza = nodo
            self.cola = nodo
        else:
            self.cola.next = nodo
            nodo.tail = self.cola
            self.cola = nodo
        self.contador+=1

#RECORRER LA LISTA
    def recorrer(self):
        actual = self.cabeza
        while actual:
            tipo_dato = actual.tipo_dato
            actual = actual.next
            yield tipo_dato

#MOSTRAR LA LISTA EN LA CONSOLA
    def mostrar(self):
        actual = self.cabeza
        print ("<----LISTA DE NODOS---->")
        while actual is not None:
            print ("-->", actual.tipo_dato)
            actual = actual.next

#MOSTRAR LA LISTA DE ATRAS PARA ADELANTE O DE FORMA INVERSA
    def mostrar_al_reves(self):
        prev = self.cola
        print ("<----LISTA DE NODOS INVERSA O AL REVÉS---->")
        while prev is not None:
            print ("-->",prev.tipo_dato)
            prev = prev.tail

#BUSCAR UN ELEMENTO EN LA LISTA    
    def buscar(self, busqueda):
        dato = self.cabeza
        print ("<----BÚSQUEDA DE DATOS--->")
        while dato is not None:
            if dato.tipo_dato == busqueda:
                print ("EL VALOR ENCONTRADO ES: -->", busqueda)
            dato = dato.next
        else:
            print("EL DATO NO EXISTE EN LA LISTA DE NODOS")

#INSERTAR UN VALOR AL INICIO DE LA LISTA
    def insertar_inicio(self, tipo_dato):
        print ("<----INSERTANDO NUEVO VALOR AL INICIO---->")
        nuevo_nodo = Nodo(tipo_dato)
        if self.cabeza is None:
            self.cabeza = nuevo_nodo
            self.cola = nuevo_nodo
        else:
            nuevo_nodo.next = self.cabeza
            self.cabeza.tail = nuevo_nodo
            self.cabeza = nuevo_nodo
        self.contador+=1
        print ("El nuevo valor a insertar es --> 4")

#ELIMINAR UN VALOR EN LA LISTA
    def eliminar_nodo(self, eliminacion):
        mochar = self.cabeza
        e = False
        print ("<----ELIMINACION DE UN NODO DE LA LISTA---->")
        while mochar is not None:
            if mochar.tipo_dato == eliminacion:
                print ("EL VALOR A ELIMINAR ES -->", eliminacion)
                if mochar == self.cabeza:
                    self.cabeza = self.cabeza.next
                    if self.cabeza:
                        self.cabeza.tail = None
                elif mochar == self.cola:
                    self.cola = self.cola.tail
                    if self.cola:    
                        self.cola.next = None
                else:
                    mochar.tail.next = mochar.next
                    mochar.next.tail = mochar.tail 
                self.contador-=1
                break
            mochar = mochar.next 

#SUMATORIA DE LOS ELEMENTOS DE LA LISTA  
    def suma_de_nodos(self):
        nodo_actual = self.cabeza
        total = 0
        print ("<----SUMATORIA DE LOS DATOS DE LOS NODOS---->")
        while nodo_actual is not None:
            total += nodo_actual.tipo_dato
            nodo_actual = nodo_actual.next
        print ("LA SUMA TOTAL DE LOS DATOS DE LOS NODOS ES -->", total)

#INSERTAR UN ELEMENTO AL FINAL DE LA LISTA
    def insetar_al_final(self, tipo_dato):
        print ("<----INSERTANDO NUEVO VALOR AL FINAL---->")
        ultimo = Nodo(tipo_dato)
        if self.cola is None:
            self.cola = ultimo
            self.cabeza = ultimo
        else:
            ultimo.tail = self.cola
            self.cola.next = ultimo
            self.cola = ultimo
        self.contador+=1
        print("El nuevo valor a insertar es --> 15")

#INSERTAR UN ELEMENTO ENTRE DOS ELEMENTOS DE LA LISTA
    def insertar_en_medio(self, añadir, nuevo_valor):
        dato = self.cabeza
        nuevo_nodo = Nodo(nuevo_valor)
        print ("<----BUSCANDO SI EL DATO EXISTE EN LA LISTA--->")
        while dato is not None:
            if dato.tipo_dato == añadir:
                print ("<----EL VALOR SI EXISTE EN LA LISTA---->")
                if dato == self.cabeza:
                    print ("<----NO SE PERMITEN AÑADIR VALORES AL INICIO DE LA LISTA DENTRO DEL CONTEXTO DE ESTA OPERACION---->")
                elif dato == self.cola:
                    print ("<----NO SE PERMITEN AÑADIR VALORES AL FINAL DE LA LISTA DENTRO DEL CONTEXTO DE ESTA OPERACION---->")
                else:
                    valor_izq = dato
                    valor_der = dato.next
                    valor_izq.next = nuevo_nodo
                    valor_der.tail = nuevo_nodo
                    nuevo_nodo.next = valor_der
                    nuevo_nodo.tail = valor_izq
                self.contador+=1
                break
            dato = dato.next
        else:
            print("EL DATO NO EXISTE EN LA LISTA DE NODOS")

#ORDENAR LISTA DE MAYOR A MENOR
    def mayor_menor(self):
        print ("<----ORDENANDO DE MAYOR A MENOR---->")
        i = 0
        while i < self.contador:
            actual = self.cabeza
            while actual.next is not None:
                if actual.tipo_dato < actual.next.tipo_dato:
                    temporal = actual.tipo_dato
                    actual.tipo_dato = actual.next.tipo_dato
                    actual.next.tipo_dato = temporal
                actual = actual.next 

            i += 1
        self.mostrar()

#ORDENAR LA LISTA DE MENOR A MAYOR
    def menor_mayor(self):
        print ("<----ORDENANDO DE MENOR A MAYOR---->")
        i = 0
        while i < self.contador:
            actual = self.cabeza
            while actual.next is not None:
                if actual.tipo_dato > actual.next.tipo_dato:
                    temporal = actual.tipo_dato
                    actual.tipo_dato = actual.next.tipo_dato
                    actual.next.tipo_dato = temporal
                actual = actual.next 

            i += 1
        self.mostrar()

#MODIFCAR EL VALOR DEL ELEMENTO EN ALGUNA DETERMINADA POSICION DE LA LISTA
    def modificar_posicion(self, modificar_valor, nuevo_dato):
        print("<----MODIFICANDO POSICION---->")
        nodo_actual = self.cabeza
        i = 0
        if modificar_valor >= self.contador:
            print ("POSICION INVALIDA")
            return
        while nodo_actual is not None:
            if i == modificar_valor:
                nodo_actual.tipo_dato = nuevo_dato
                break
            nodo_actual = nodo_actual.next
            i += 1
        print("<----LISTA DE NODOS CON EL VALOR MODIFICADO---->")   
            

numeros=Mi_lista_doble()
numeros.insertar(1)
numeros.insertar(6)
numeros.insertar(3)
numeros.insertar(2)
print("\n")
numeros.mostrar()
print("\n")
numeros.mostrar_al_reves()
print("\n")
numeros.buscar(25)
print("\n")
print("Cantidad de nodos en la lista:", numeros.contador)
print("\n")
numeros.insertar_inicio(4)
print("\n")
numeros.mostrar()
print ("\n")
numeros.eliminar_nodo(3)
print("\n")
numeros.mostrar()
print("\n")
numeros.suma_de_nodos()
print("\n")
numeros.insetar_al_final(15)
print("\n")
numeros.mostrar()
print("\n")
numeros.insertar_en_medio(6, 20)
print("\n")
numeros.mostrar()
print("\n")
numeros.mayor_menor()
print("\n")
numeros.menor_mayor()
print("\n")
numeros.modificar_posicion(20, 36)
print("\n")
numeros.mostrar()
