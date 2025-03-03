package ProyectBiblioteca;


public class Libro {
    // atributos 
    private String titulo;
    private String autor;
    private String ISBN ;
    private int anio;
    private int copias;

    //metodo constructor que nos permite inicializar los atributos del objeto
    public Libro(String titulo, String autor, String ISBN, int anio, int copias) {
        this.titulo = titulo;
        this.autor = autor;
        this.ISBN = ISBN;
        this.anio = anio;
        this.copias = copias;
    }
// getter que nos permite acceder a los valores de los atributos
    public String getTitulo() {
        return titulo;
    }

    public String getAutor() {
        return autor;
    }

    public String getISBN() {
        return ISBN;
    }

    public int getAnio() {
        return anio;
    }

    public int getCopias() {
        return copias;
    }
// setter que nos permiten modificar los valores de los atributos privados.
    public void setTitulo(String titulo) {
        this.titulo = titulo;
    }

    public void setAutor(String autor) {
        this.autor = autor;
    }

    public void setISBN(String ISBN) {
        this.ISBN = ISBN;
    }

    public void setAnio(int anio) {
        this.anio = anio;
    }

    public void setCopias(int copias) {
        this.copias = copias;
    }
// toString convierte en un objeto en una cadena de texto
    @Override
    public String toString() {
        return "Libro{\n" + 
           "titulo=" + titulo + "\n" + 
           " autor=" + autor + "\n" + 
           " ISBN=" + ISBN + "\n" + 
           " anio=" + anio + "\n" + 
           " copias=" + copias + "\n" + 
           '}';
    }

    package ProyectBiblioteca;

import java.util.ArrayList;

public class Biblioteca {

    // usamos un ArrayList llamado ListaLibros para almecenar libros.
    private ArrayList<Libro> listaLibros;

    //inicializa la lista de un libro como ArrayLisVacio
    public Biblioteca() {
        listaLibros = new ArrayList<>();
    }
//

    public boolean agregarLibro(Libro l) {
        if (l == null) { // verifica si el libro es null
            return false;
        }
        for (int i = 0; i < listaLibros.size(); i++) {
            if (listaLibros.get(i).getTitulo().equalsIgnoreCase(l.getTitulo())) {
                return false; // No se agregan duplicados
            }
            if (listaLibros.get(i).getTitulo().compareToIgnoreCase(l.getTitulo()) > 0) {
                listaLibros.add(i, l);
                return true;
            }
        }
        return listaLibros.add(l);
    }
    // Buscar libro por titulo

    public int buscarLibro(String titulo) {
        for (int i = 0; i < listaLibros.size(); i++) {
            if (listaLibros.get(i).getTitulo().equalsIgnoreCase(titulo)) {
                return i; // Devuelve la posicion en la lista
            }
        }
        return -1; // retorna -1 si No lo encuentra
    }

    // Contar libros sin copias
    public int nLibrosSinCopias() {
        int contador = 0;
        for (Libro l : listaLibros) {
            if (l.getCopias() == 0) {
                contador++;
            }
        }
        return contador;
    }

    @Override
    public String toString() {
         return "Biblioteca{\n" + "Libros=" + listaLibros + "\n}";
    }
}

package ProyectBiblioteca;

public class Prueba {

    public static void main(String[] args) {

        // Crear libros
        Libro libro1 = new Libro("Perdona si te llamo amor", "Federico Moccia", "123456", 1992 , 5);
        Libro libro2 = new Libro("Tres Metros Sobre el Cielo", "Federico M", "789101", 1993, 2);
        Libro libro3 = new Libro("Don Quijote de la Mancha", "Miguel de Cervantes", "111213", 1605, 0);

        // Crear biblioteca
        Biblioteca biblioteca = new Biblioteca();

        // Agregar libros
        biblioteca.agregarLibro(libro1);
        biblioteca.agregarLibro(libro2);
        biblioteca.agregarLibro(libro3);

        // Mostrar biblioteca
        System.out.println("Biblioteca después de agregar libros:");
        System.out.println(biblioteca);

        // Buscar un libro
        String tituloBuscado = "El Principito";
        int posicion = biblioteca.buscarLibro(tituloBuscado);
        if (posicion != -1) {
            System.out.println("El libro '" + tituloBuscado + "' está en la posición " + posicion);
        } else {
            System.out.println("El libro '" + tituloBuscado + "' no está en la biblioteca.");
        }

        // Contar libros sin copias
        System.out.println("Número de libros sin copias: " + biblioteca.nLibrosSinCopias());
    }
}

    
