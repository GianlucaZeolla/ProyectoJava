import java.io.*;
import java.util.InputMismatchException;
import java.util.LinkedList;
import java.util.Scanner;


class TalleInvalidoException extends Exception {
    private int talle;

    // Define una excepción propia para el caso de un talle de zapatilla incorrecto.
    public TalleInvalidoException(int talle) {
        super("Talle inválido: " + talle + ". El talle debe estar entre 20 y 50.");
        this.talle = talle;
    }

    public int getTalle() {
        return talle;
    }
}

class Zapatilla implements Serializable {
    private String marca;
    private int talle;
    private double precio;

    public Zapatilla(String marca, int talle, double precio) {
        this.marca = marca;
        this.talle = talle;
        this.precio = precio;
    }


    public String getMarca() {
        return marca;
    }

    public void setMarca(String marca) {
        this.marca = marca;
    }

    public int getTalle() {
        return talle;
    }

    public void setTalle(int talle) {
        this.talle = talle;
    }

    public double getPrecio() {
        return precio;
    }

    public void setPrecio(double precio) {
        this.precio = precio;
    }
}

public class Main {
    public static void main(String[] args) {
        LinkedList<Zapatilla> zapatillas = new LinkedList<>();
        Scanner scanner = new Scanner(System.in);


        int opcion;


        do {

            System.out.println("--------------------------------------");
            System.out.println("Menu de opciones");
            System.out.println("1. Agregar zapatilla");
            System.out.println("2. Mostrar contenido del LinckedList");
            System.out.println("3. Guardar en archivo");
            System.out.println("4. leer desde el archivo");
            System.out.println("5. Mostrar contenidos del archivo");
            System.out.println("6. Salir");
            System.out.println("--------------------------------------");
            System.out.print("Ingrese una opcion:");

            opcion = scanner.nextInt();

            switch (opcion) {
                case 1:
                    agregarZapatilla(zapatillas, scanner);
                    break;
                case 2:
                    mostrarLickedList(zapatillas);
                    break;
                case 3:
                    guardarArchivo(zapatillas);
                    break;
                case 4:
                    leerArchivo(zapatillas);
                    break;
                case 5:
                    mostrarArchivo(zapatillas);
                    break;
                case 6:
                    break;
                default:
                    // Lanza una excepción si se encuentra un valor inesperado en la variable 'opcion'.
                    throw new IllegalStateException("Unexpected value: " + true);
            }

        } while (opcion != 6);

    }


    private static void agregarZapatilla(LinkedList<Zapatilla> zapatillas, Scanner scanner) {
        try {


            System.out.print("Ingresa la marca de la zapatilla: ");
            String nombreMarca = scanner.next();


            System.out.print("Ingresa el talle: ");
            int talle = scanner.nextInt();
            validarTalle(talle); // Validar el talle antes de crear la zapatilla


            System.out.print("Ingresa el precio: ");
            double precio = scanner.nextDouble();

            Zapatilla nuevaZapatilla = new Zapatilla(nombreMarca, talle, precio);
            zapatillas.add(nuevaZapatilla);
            System.out.println("Zapatilla agregada correctamente.");

        } catch (InputMismatchException e) {
            System.out.println("Caracter incorrecto");

        } catch (TalleInvalidoException e) {
            System.out.println(e.getMessage());
            System.out.println("El talle ingresado fue: " + e.getTalle());
        }

    }

    private static void validarTalle(int talle) throws TalleInvalidoException {
        if (talle < 20 || talle > 50) {
            // Lanza una excepción propia indicando que el talle está fuera del rango permitido.
            throw new TalleInvalidoException(talle);
        }
    }

    private static void mostrarLickedList(LinkedList<Zapatilla> zapatillas) {
            for (Zapatilla z: zapatillas) {


                System.out.println("Marca: " + z.getMarca() + " Talle: " + z.getTalle() + " Precio: " + z.getPrecio());

            }
        }
    private static void guardarArchivo(LinkedList<Zapatilla> zapatillas) {
        try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("src/ObjetosZapatillas.dat"))) {
            // Escribe la lista de zapatillas en el archivo
            out.writeObject(zapatillas);
            // Captura cualquier excepción de tipo IOException que pueda ocurrir durante la escritura
            System.out.println("Zapatillas guardadas en el archivo");
        } catch (IOException e) {
            // Captura la excepcion si no se puede encontrar el archivo especificado en FileOutputStream
            e.printStackTrace();
        }
    }


    private static void leerArchivo(LinkedList<Zapatilla> zapatillas) {
        try (ObjectInputStream in = new ObjectInputStream(new FileInputStream("src/ObjetosZapatillas.dat"))) {
            LinkedList<Zapatilla> zapatillasLeidas = (LinkedList<Zapatilla>) in.readObject();
            zapatillas.addAll(zapatillasLeidas);
            System.out.println("Zapatillas leidas desde el archivo");
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }

    private static void mostrarArchivo(LinkedList<Zapatilla> zapatillas) {
        System.out.println("Contenido del Archivo:");
        mostrarLickedList(zapatillas);
    }
}
