# Tarea 7 - Excepciones

## 1. Indica cuál es el nombre de la clase Java que define las excepciones, y de la que debe heredar cualquier clase que queramos usar para representar una excepción.
    El nombre de la clase Java que define las excepciones es Throwable, y cualquier clase que queramos usar para representar una excepción debe heredar de esta clase.

## 2. ¿Cuál es el nombre de la clase Java que representa las excepciones producidas al invocar a un método de un objeto cuyo valor es “null”?
    El nombre de la clase Java que representa las excepciones producidas al invocar a un método de un objeto cuyo valor es “null” es NullPointerException.

## 3. Observa el siguiente fragmento de código e indica si se produce alguna excepción. En caso afirmativo indica cuál:
```java
    String [] arrayString = new String[25];
    System.out.println(arrayString[3].length());
```
    Sí, se produce una excepción. La excepción que se produce es NullPointerException, ya que se está intentando acceder a un método de un objeto que no ha sido inicializado.

## 4. Observa el siguiente fragmento de código e indica qué sucederá al ejecutar el mismo.
```java
    String aux = "hola";
    int aux2 = Integer.parseInt(aux);
```

    Al ejecutar el código se producirá una excepción. La excepción que se producirá es NumberFormatException, ya que se está intentando convertir una cadena de caracteres que no representa un número a un entero.

## 5. El siguiente código produce excepciones:
```java
    public static void main(String[] args) {
        String texto = "Test";
        int divisor = Integer.parseInt(texto);
        System.out.println(3 / 0);
    }
```

### a. ¿De qué tipo son?
    Las excepciones que se producen son de tipo NumberFormatException y ArithmeticException.
### b. ¿Son checked or unchecked?
    Las excepciones son unchecked.
### c. Crea dos métodos e inserta el texto que genera la excepción en cada uno de ellos. Por  ejemplo: un método que contenga System.out.println(3 / 0); y otro método que  contenga el otro texto que genera la otra excepción. Cada uno de los métodos debe  manejar la excepción con su respectivo try-catch. Desde el main invoca los dos  métodos.
```java
public class Main {
    public static void main(String[] args) {
        metodo1();
        metodo2();
    }

    public static void metodo1() {
        try {
            System.out.println(3 / 0);
        } catch (ArithmeticException e) {
            System.out.println("No se puede dividir por cero");
        }
    }

    public static void metodo2() {
        try {
            String texto = "Test";
            int divisor = Integer.parseInt(texto);
        } catch (NumberFormatException e) {
            System.out.println("No se puede convertir una cadena de caracteres que no representa un número a un entero");
        }
    }
}
```
### d. Ahora elimina los try-catch de los métodos y captúralas en el main. ¿Cuántos bloques trycatch has necesitado para capturar ambas?
    Se necesitaron dos bloques try-catch para capturar ambas excepciones.

## 6. Dado el siguiente programa en Java modifícalo y trata las excepciones que se puedan producir.

```java
public class Ejercicio6 {
 static Scanner sc = new Scanner(System.in);
 public static void main(String[] args) {
 double n;
 int posicion;
 String cadena ;
 double[] valores = {9.83, 4.5, -3.06, 0.06, 2.52, -11.3, 7.60, 3.00, -30.4, 105.2};
 System.out.println("Contenido del array antes de modificar:");
 for (int i = 0; i < valores.length; i++) {
 System.out.printf("%.2f ", valores[i]);
 }
 System.out.print("\n\nIntroduce la posición del array a modificar: ");
 cadena = sc.nextLine();
 posicion = Integer.parseInt(cadena);
 System.out.print("\nIntroduce el nuevo valor de la posición " + posicion + ": ");
 n = sc.nextDouble();
 valores[posicion] = n;
 System.out.println("\nPosición a modificar " + posicion);
 System.out.println("Nuevo valor: " + n);
 System.out.println("Contenido del array modificado:");
 for (int i = 0; i < valores.length; i++) {
 System.out.printf("%.2f ", valores[i]);
 }
 }
}
```

    Corregido

```java 
public class Ejercicio6 {
    static Scanner sc = new Scanner(System.in);
    public static void main(String[] args) {
        double n;
        int posicion;
        String cadena ;
        double[] valores = {9.83, 4.5, -3.06, 0.06, 2.52, -11.3, 7.60, 3.00, -30.4, 105.2};
        System.out.println("Contenido del array antes de modificar:");
        for (int i = 0; i < valores.length; i++) {
            System.out.printf("%.2f ", valores[i]);
        }
        System.out.print("\n\nIntroduce la posición del array a modificar: ");
        try {
            cadena = sc.nextLine();
            posicion = Integer.parseInt(cadena);
            System.out.print("\nIntroduce el nuevo valor de la posición " + posicion + ": ");
            n = sc.nextDouble();
            valores[posicion] = n;
            System.out.println("\nPosición a modificar " + posicion);
            System.out.println("Nuevo valor: " + n);
            System.out.println("Contenido del array modificado:");
            for (int i = 0; i < valores.length; i++) {
                System.out.printf("%.2f ", valores[i]);
            }
        } catch (NumberFormatException e) {
            System.out.println("La posición debe ser un número entero");
        } catch (ArrayIndexOutOfBoundsException e) {
            System.out.println("La posición debe ser un número entero entre 0 y " + (valores.length - 1));
        } catch (InputMismatchException e) {
            System.out.println("El valor debe ser un número decimal");
        }
    }
}
```

## 7. Crea la siguiente clase en la que las propiedades no permitan argumentos ilegales lanzando excepciones. Clase Persona:
## Propiedades:
### dni: El dni tiene que ser correcto. Podéis utilizar la función ya programada para comprobarlo
### edad: Tiene que ser mayor o igual que 0
### nombre: Tiene que estar formado por al menos tres palabras correspondientes al nombre y los  dos apellidos
## Crea un main probando la clase y capturando las excepciones que pueda generar la clase en caso de asignar los valores incorrectos.

```java
public class Persona {
    private String dni;
    private int edad;
    private String nombre;

    public Persona(String dni, int edad, String nombre) {
        if (!comprobarDni(dni)) {
            throw new IllegalArgumentException("El DNI no es correcto");
        }
        if (edad < 0) {
            throw new IllegalArgumentException("La edad no puede ser negativa");
        }
        if (!comprobarNombre(nombre)) {
            throw new IllegalArgumentException("El nombre no es correcto");
        }
        this.dni = dni;
        this.edad = edad;
        this.nombre = nombre;
    }

    public String getDni() {
        return dni;
    }

    public void setDni(String dni) {
        if (!otraPractica.comprobarDni(dni)) {
            throw new IllegalArgumentException("El DNI no es correcto");
        }
        this.dni = dni;
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        if (edad < 0) {
            throw new IllegalArgumentException("La edad no puede ser negativa");
        }
        this.edad = edad;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        if (!otraPractica.comprobarNombre(nombre)) {
            throw new IllegalArgumentException("El nombre no es correcto");
        }
        this.nombre = nombre;
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
        try {
            Persona persona = new Persona("12345678Z", 25, "Juan Pérez Gómez");
            System.out.println("DNI: " + persona.getDni());
            System.out.println("Edad: " + persona.getEdad());
            System.out.println("Nombre: " + persona.getNombre());
        } catch (IllegalArgumentException e) {
            System.out.println(e.getMessage());
        }
    }
}
```
