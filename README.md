# Arrays

PostgreSQL permite o uso de arrays. A información sobre este tipo de datos tédela no seguinte enlace: (https://www.postgresql.org/docs/9.1/arrays.html)[https://www.postgresql.org/docs/9.1/arrays.html].

Vamos ver un exemplo de como insertar arrays nunha táboa. Na documentación do enlace anterior tedes ademais como realizar consultas sobre estes arrays.

## Exemplo

Creamos a táboa:
```java
String sqlTableCreation = new String(
    "CREATE TABLE IF NOT EXISTS probaarrays ("
            + "id SERIAL PRIMARY KEY, "
            + "numeros INTEGER[], "
            + "mensaxes TEXT[]);");
CallableStatement createTable = conn.prepareCall(sqlTableCreation);
createTable.execute();
createTable.close();
```

Para poder engadir un array de obxectos de JAVA hai que transformar ese array co seguinte método **Array createArrayOf(String typeName, Object[] elements) throws SQLException**.

```java
String insertSQL = new String(
    "INSERT INTO probaarrays(numeros,mensaxes) VALUES(?,?)");
PreparedStatement insert = conn.prepareStatement(insertSQL);

Integer[] num = {1,2,3,4,5,6,7};
String[] men = {"Acceso","a","datos"};

insert.setArray(1, conn.createArrayOf("INTEGER", num));
insert.setArray(2, conn.createArrayOf("TEXT", men));

insert.execute();
insert.close();   
```
