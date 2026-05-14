## Interactuar con la Base de Datos

Para interactuar con la base de datos, usaremos **tres clases principales** (para SQLite):

- **SqliteConnection** : Establece la conexión con el archivo de la base de datos.
- **SqliteCommand** : Representa la orden SQL que vamos a ejecutar.
- **SqliteDataReader** : Nos permite leer los resultados de una consulta SELECT fila 
por fila.

## Flujo de trabajo

1. Crear conexión
```csharp
using (SqliteConnection conexion = new SqliteConnection(cadena))
```
2. Open() → OPEN
```csharp
conexion.Open();
```
3. Usar BD → OK
```csharp
using (SqliteConnection conexion = new SqliteConnection(cadena))
SqliteCommand comando = conexion.CreateCommand();
comando.CommandText = "CREATE TABLE IF NOT EXISTS Personas (Nombre TEXT);";
comando.ExecuteNonQuery();
```
4. Salir de using → CLOSE automático

## ¿Cómo ejecutar las consultas SQL?

1. Primero se crea el comando:
```csharp
SqliteCommand comando = conexion.CreateCommand();
comando.CommandText = "CREATE TABLE IF NOT EXISTS Personas (Nombre TEXT);";
```
2. A continuación llamamos al comando para ejecutar:
   
    - **comando.ExecuteNonQuery**: para INSERT, UPDATE, DELETE
    - **comando.ExecuteReader**: para sentencias SELECT
    - **comando.ExecuteScalar()**: Para sentencias SELECT que devuelven un único valor (ej: COUNT(*) ).