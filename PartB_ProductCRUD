import java.sql.*;
import java.util.Scanner;

public class PartB_ProductCRUD {
    public static void main(String[] args) {
        String url = "jdbc:mysql://localhost:3306/companydb";
        String user = "root";
        String password = "root";

        try (Connection con = DriverManager.getConnection(url, user, password);
             Scanner sc = new Scanner(System.in)) {

            Class.forName("com.mysql.cj.jdbc.Driver");
            con.setAutoCommit(false);

            while (true) {
                System.out.println("\n--- Product Menu ---");
                System.out.println("1. Insert Product");
                System.out.println("2. View Products");
                System.out.println("3. Update Product");
                System.out.println("4. Delete Product");
                System.out.println("5. Exit");
                System.out.print("Enter choice: ");
                int ch = sc.nextInt();

                switch (ch) {
                    case 1:
                        System.out.print("Enter Product ID: ");
                        int id = sc.nextInt();
                        System.out.print("Enter Product Name: ");
                        String name = sc.next();
                        System.out.print("Enter Price: ");
                        double price = sc.nextDouble();
                        System.out.print("Enter Quantity: ");
                        int qty = sc.nextInt();

                        PreparedStatement ps1 = con.prepareStatement("INSERT INTO Product VALUES (?, ?, ?, ?)");
                        ps1.setInt(1, id);
                        ps1.setString(2, name);
                        ps1.setDouble(3, price);
                        ps1.setInt(4, qty);
                        ps1.executeUpdate();
                        con.commit();
                        System.out.println("Product added successfully!");
                        break;

                    case 2:
                        Statement stmt = con.createStatement();
                        ResultSet rs = stmt.executeQuery("SELECT * FROM Product");
                        System.out.println("ID\tName\tPrice\tQty");
                        while (rs.next()) {
                            System.out.println(rs.getInt(1) + "\t" + rs.getString(2) + "\t" +
                                               rs.getDouble(3) + "\t" + rs.getInt(4));
                        }
                        rs.close();
                        break;

                    case 3:
                        System.out.print("Enter Product ID to update: ");
                        int uid = sc.nextInt();
                        System.out.print("Enter new Price: ");
                        double newPrice = sc.nextDouble();
                        PreparedStatement ps2 = con.prepareStatement("UPDATE Product SET Price=? WHERE ProductID=?");
                        ps2.setDouble(1, newPrice);
                        ps2.setInt(2, uid);
                        ps2.executeUpdate();
                        con.commit();
                        System.out.println("Product updated successfully!");
                        break;

                    case 4:
                        System.out.print("Enter Product ID to delete: ");
                        int did = sc.nextInt();
                        PreparedStatement ps3 = con.prepareStatement("DELETE FROM Product WHERE ProductID=?");
                        ps3.setInt(1, did);
                        ps3.executeUpdate();
                        con.commit();
                        System.out.println("Product deleted successfully!");
                        break;

                    case 5:
                        System.out.println("Exiting...");
                        return;
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
