# Tarea3-Ingreso-de-libros-en-archivos-de-texto-
Tarea 3 Ingreso de libros en archivos de texto, con las capturas pedidas
using System;

namespace EjercicioLibros
{
    public class Libros
    {
        // Propiedades requeridas
        public string Codigo { get; set; }
        public string Titulo { get; set; }
        public string Autor { get; set; }
        public int Year { get; set; }
        public string Editorial { get; set; }
        public int NumeroPaginas { get; set; }

        // Constructor vacío
        public Libros() { }

        public Libros(string codigo, string titulo, string autor, int year, string editorial, int numeroPaginas)
        {
            Codigo = codigo;
            Titulo = titulo;
            Autor = autor;
            Year = year;
            Editorial = editorial;
            NumeroPaginas = numeroPaginas;
        }
        public string ObtenerDetalles()
        {
            return $"Código: {Codigo}\n" +
                   $"Título: {Titulo}\n" +
                   $"Autor: {Autor}\n" +
                   $"Año: {Year}\n" +
                   $"Editorial: {Editorial}\n" +
                   $"Número de páginas: {NumeroPaginas}\n";
        }
    }
}
   // 2. SEGUNDA CLASE: Que es donde corre el programa
    class Program
    {
        static void Main(string[] args)
        {
            int cantidadLibros = 5;
            Libros[] arregloLibros = new Libros[cantidadLibros];

            Console.WriteLine("=== INGRESO DE DATOS DE LIBROS ===");

            for (int i = 0; i < cantidadLibros; i++)
            {
                Console.WriteLine($"\n--- Registro: Libro {i + 1} ---");

                Console.Write("Código: ");
                string codigo = Console.ReadLine();

                Console.Write("Título: ");
                string titulo = Console.ReadLine();

                Console.Write("Autor: ");
                string autor = Console.ReadLine();

                Console.Write("Año de publicación: ");
                int year = int.Parse(Console.ReadLine());

                Console.Write("Editorial: ");
                string editorial = Console.ReadLine();

                Console.Write("Número de páginas: ");
                int paginas = int.Parse(Console.ReadLine());

                arregloLibros[i] = new Libros(codigo, titulo, autor, year, editorial, paginas);
            }

            Console.WriteLine("\n=================================");
            Console.WriteLine("   DATOS DE LIBROS REGISTRADOS   ");
            Console.WriteLine("=================================");

            for (int i = 0; i < arregloLibros.Length; i++)
            {
                Console.WriteLine($"--- Libro {i + 1} ---");
                Console.WriteLine(arregloLibros[i].ObtenerDetalles());
            }

            string rutaArchivo = "libros.txt";

            try
            {
                using (StreamWriter escritor = new StreamWriter(rutaArchivo))
                {
                    escritor.WriteLine("=== REGISTRO DE LIBROS ===");
                    for (int i = 0; i < arregloLibros.Length; i++)
                    {
                        escritor.WriteLine($"Libro {i + 1}");
                        escritor.WriteLine(arregloLibros[i].ObtenerDetalles());
                        escritor.WriteLine("---------------------------------");
                    }
                }

                Console.WriteLine($"\n¡Los datos se guardaron exitosamente en '{rutaArchivo}'!");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Ocurrió un error al guardar el archivo: {ex.Message}");
            }

            Console.WriteLine("\nPresiona cualquier tecla para salir...");
            Console.ReadKey();
        }
    }
