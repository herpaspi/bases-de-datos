
```csharp
using System;
using Microsoft.Data.Sqlite;

class Program
{
    static void Main()
    {
        string cadena = "Data Source=miBD.db";

        using (SqliteConnection conexion = new SqliteConnection(cadena))
        {
            conexion.Open();

            // Crear tabla
            SqliteCommand comando = conexion.CreateCommand();
            comando.CommandText = "CREATE TABLE IF NOT EXISTS Personas" + 
                                  " (id INTEGER PRIMARY KEY AUTOINCREMENT" +
                                  ", Nombre TEXT, Edad INTEGER);";
            comando.ExecuteNonQuery();


            // Insertar dato
            SqliteCommand insertar = conexion.CreateCommand();
            insertar.CommandText = "INSERT INTO Personas (Nombre, Edad)"+
                                    " VALUES ('Ana',30);";
            insertar.ExecuteNonQuery();

            // Leer datos
            SqliteCommand leer = conexion.CreateCommand();
            leer.CommandText = "SELECT * FROM Personas;";

            using (SqliteDataReader datos = leer.ExecuteReader())
            {
                while (datos.Read())
                {
                    string nombre = Convert.ToString(datos[1]);
                    int edad = Convert.ToInt32(datos[2]);
                    Console.WriteLine(nombre + " - " + edad);
                }
            }
        }
    }
}
```