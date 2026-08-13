# JavaMySQLCRUD.java
import java.sql.*;

public class JavaMySQLCRUD {

    static final String URL = "jdbc:mysql://localhost:3306/crud_application";
    static final String USER = "root";
    static final String PASSWORD = "your_password";

    public static void main(String[] args) {

        try {
            Connection connection =
                DriverManager.getConnection(URL, USER, PASSWORD);

            System.out.println("Connected to MySQL successfully!");

            // CREATE
            String insertSQL =
                "INSERT INTO students (name, surname, email) VALUES (?, ?, ?)";

            PreparedStatement insert =
                connection.prepareStatement(insertSQL);

            insert.setString(1, "Lemogang");
            insert.setString(2, "Seloane");
            insert.setString(3, "lemogang@example.com");

            insert.executeUpdate();
            System.out.println("Student added.");

            // READ
            String selectSQL = "SELECT * FROM students";
            Statement statement = connection.createStatement();
            ResultSet result = statement.executeQuery(selectSQL);

            System.out.println("\nStudents:");

            while (result.next()) {
                System.out.println(
                    result.getInt("id") + " - " +
                    result.getString("name") + " " +
                    result.getString("surname") + " - " +
                    result.getString("email")
                );
            }

            // UPDATE
            String updateSQL =
                "UPDATE students SET email=? WHERE id=?";

            PreparedStatement update =
                connection.prepareStatement(updateSQL);

            update.setString(1, "updated@example.com");
            update.setInt(2, 1);

            update.executeUpdate();
            System.out.println("\nStudent updated.");

            // DELETE
            String deleteSQL =
                "DELETE FROM students WHERE id=?";

            PreparedStatement delete =
                connection.prepareStatement(deleteSQL);

            delete.setInt(1, 1);

            delete.executeUpdate();
            System.out.println("Student deleted.");

            connection.close();

        } catch (SQLException e) {
            System.out.println("Database error: " + e.getMessage());
        }
    }
}
