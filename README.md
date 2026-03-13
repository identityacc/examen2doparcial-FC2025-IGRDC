# examen2doparcial-FC2025-IGRDC

using System;

namespace SistemaDeInventario
{
    public class Producto
    {
        private string nombre;
        private string codigo;
        private double precio;
        private int cantidad;

        public Producto(string nombre, string codigo, double precio, int cantidad)
        {
            this.nombre = nombre;
            this.codigo = codigo;
            this.precio = precio;
            this.cantidad = cantidad;
        }

        public string Nombre
        {
            get { return nombre; }
            set { nombre = value; }
        }

        public string Codigo
        {
            get { return codigo; }
            set { codigo = value; }
        }

        public double Precio
        {
            get { return precio; }
            set { precio = value; }
        }

        public int Cantidad
        {
            get { return cantidad; }
            set { cantidad = value; }
        }

        public void MostrarProducto()
        {
            Console.WriteLine("Producto: " + Nombre);
            Console.WriteLine("Codigo: " + Codigo);
            Console.WriteLine("Precio: " + Precio);
            Console.WriteLine("Cantidad: " + Cantidad);
        }

        public virtual double CalcularImpuesto()
        {
            return 0;
        }
    }

    public class ProductoElectronico : Producto
    {
        private int garantiaMeses;

        public ProductoElectronico(string nombre, string codigo, double precio, int cantidad, int garantiaMeses)
            : base(nombre, codigo, precio, cantidad)
        {
            this.garantiaMeses = garantiaMeses;
        }

        public int GarantiaMeses
        {
            get { return garantiaMeses; }
            set { garantiaMeses = value; }
        }

        public override double CalcularImpuesto()
        {
            return Precio * 0.18;
        }

        public void MostrarElectronico()
        {
            MostrarProducto();
            Console.WriteLine("Garantia: " + GarantiaMeses + " meses");
            Console.WriteLine("Impuesto: " + CalcularImpuesto());
        }
    }

    public class ProductoAlimento : Producto
    {
        private DateTime fechaVencimiento;

        public ProductoAlimento(string nombre, string codigo, double precio, int cantidad, DateTime fechaVencimiento)
            : base(nombre, codigo, precio, cantidad)
        {
            this.fechaVencimiento = fechaVencimiento;
        }

        public DateTime FechaVencimiento
        {
            get { return fechaVencimiento; }
            set { fechaVencimiento = value; }
        }

        public override double CalcularImpuesto()
        {
            return Precio * 0.08;
        }

        public void MostrarAlimento()
        {
            MostrarProducto();
            Console.WriteLine("Fecha de vencimiento: " + FechaVencimiento.ToShortDateString());
            Console.WriteLine("Impuesto: " + CalcularImpuesto());
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // producto electrónico
            ProductoElectronico telefono = new ProductoElectronico(
                "POCO X6 Pro 5G",
                "E1001",
                17500,
                1,
                6
            );

            // producto alimento
            ProductoAlimento sandia = new ProductoAlimento(
                "Sandia",
                "A1001",
                500,
                1,
                new DateTime(2026, 4, 20)
            );

            Console.WriteLine("=== Producto Electronico ===");
            telefono.MostrarElectronico();

            Console.WriteLine();

            Console.WriteLine("=== Producto Alimento ===");
            sandia.MostrarAlimento();

            Console.ReadKey();
        }
    }
}
