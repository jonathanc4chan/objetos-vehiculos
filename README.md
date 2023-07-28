# objetos-vehiculos

package proyecto;


import java.util.Scanner;

public class CarreraDeCarros {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Bienvenido a la aplicación para calcular la velocidad promedio de vehículos de carreras.");

        int numCarros;
        do {
            System.out.print("Ingrese el número de carros en la competencia (debe ser mayor a 0): ");
            numCarros = scanner.nextInt();
        } while (numCarros <= 0);

        Carro[] carros = new Carro[numCarros];

        for (int i = 0; i < numCarros; i++) {
            System.out.println("\nCarro " + (i + 1));
            System.out.print("Ingrese el nombre del carro: ");
            String nombreCarro = scanner.next();
            carros[i] = new Carro(nombreCarro);

            int numVueltas;
            do {
                System.out.print("Ingrese el número de vueltas recorridas por el carro (debe ser mayor a 0): ");
                numVueltas = scanner.nextInt();
            } while (numVueltas <= 0);

            int vuelta = 1;
            while (vuelta <= numVueltas) {
                System.out.print("Ingrese la velocidad en metros/segundo de la vuelta " + vuelta + ": ");
                double velocidadVuelta = scanner.nextDouble();
                carros[i].agregarVelocidad(velocidadVuelta);
                vuelta++;
            }
        }

        System.out.println("\nResultados:");
        for (int i = 0; i < numCarros; i++) {
            double velocidadPromedio = carros[i].calcularVelocidadPromedio();
            System.out.println(carros[i].getNombre() + ": Velocidad Promedio = " + velocidadPromedio + " m/s");
        }
    }
}

class Carro {
    private String nombre;
    private double sumVelocidades;
    private int numVueltas;

    public Carro(String nombre) {
        this.nombre = nombre;
        this.sumVelocidades = 0;
        this.numVueltas = 0;
    }

    public void agregarVelocidad(double velocidad) {
        sumVelocidades += velocidad;
        numVueltas++;
    }

    public double calcularVelocidadPromedio() {
        // Suponemos que la longitud del circuito es constante para todos los carros.
        double longitudCircuito = 4000; // Longitud del circuito en metros
        return sumVelocidades / (numVueltas * longitudCircuito);
    }

    public String getNombre() {
        return nombre;
    }
}
