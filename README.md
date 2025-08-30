# Internshiptask
**1.Explain the difference between driver.get() and driver.navigate().to() in Selenium WebDriver.**

**driver.get(url)**:Opens a web page.
Wait until the page is fully loaded.
Commonly used for starting a test on a URL.
**driver.navigate().to(url)**:Similar to get()but allows additional navigation commands like back(), forward(), refresh().
Doesn't necessarily wait for the page to fully load.
**In short: get()= load page, navigate().to()= navigate + load page.**

**2.Automate the process of searching for a product and applying various filters like brand, price range, and customer ratings and price should be above 2k , customer rating should be above 4 and brand name should start with letter C. and this testing should work only between 3PM to 6PM.**




import java.time.*;
import java.util.*;

class Product {
    String name;
    String brand;
    int price;
    double rating;
      
       Product(String name, String brand, int price, double rating) {
         this.name = name;
        this.brand = brand;
        this.price = price;
        this.rating = rating;
    }
}

public class AmazonFilterSimulation {
    public static void main(String[] args) {
        // Allowed time window
        LocalTime start = LocalTime.of(15, 0);  // 3PM
        LocalTime end = LocalTime.of(18, 0);    // 6PM
        LocalTime now = LocalTime.now();

        if (now.isBefore(start) || !now.isBefore(end)) {
            System.out.println("[SKIPPED] Test only runs between 3PM and 6PM. Current time: " + now);
            return;
        }

        // Simulated products (pretend from Amazon)
        List<Product> products = Arrays.asList(
            new Product("Gaming Laptop", "Canon", 2500, 4.5),
            new Product("Business Laptop", "Dell", 2200, 4.3),
            new Product("Ultrabook", "Creative", 3000, 4.7),
            new Product("Tablet", "Apple", 1500, 4.8)
        );

        // Apply filters: Brand starts with 'C', price > 2000, rating > 4
        char brandInitial = 'C';
        int minPrice = 2000;
        double minRating = 4.0;

        System.out.println("=== Filtered Results ===");
        for (Product p : products) {
            if (p.price > minPrice &&
                p.rating > minRating &&
                p.brand.toUpperCase().startsWith(String.valueOf(brandInitial))) {
                System.out.printf("Product: %s | Brand: %s | $%d | %.1f★%n",
                                  p.name, p.brand, p.price, p.rating);
            }
        }
    }
}

  **3.Automate a system that monitors price changes for a product and triggers a notification (eg, email) when it drops below a certain threshold.**
  
  
  import java.util.*;

public class PriceMonitorDemo {

    private static final double PRICE_THRESHOLD = 2000.00;

    public static void main(String[] args) {
        // Simulated product data
        String productName = "Gaming Laptop";
        String productUrl = "https://example.com/product";

        // Simulate fetching current price (random between 1500–3000)
        double currentPrice = 1500 + new Random().nextInt(1500);

        System.out.println("Monitoring product: " + productName);
        System.out.println("Current price: $" + currentPrice);
        System.out.println("Threshold: $" + PRICE_THRESHOLD);

        // Check if below threshold
        if (currentPrice < PRICE_THRESHOLD) {
            triggerNotification(productName, productUrl, currentPrice);
        } else {
            System.out.println("No alert. Price is above threshold.");
        }
    }

    // Simulated notification (just prints in console)
    private static void triggerNotification(String product, String url, double price) {
        System.out.println("=== NOTIFICATION TRIGGERED ===");
        System.out.println("Price dropped for: " + product);
        System.out.println("New Price: $" + price);
        System.out.println("Check product here: " + url);
    }
}


**4.Automate adding multiple products to the shopping cart and verifying the total price and the total price should be more than 2000 rupees and user name should contain only 10 characters and should not have any special characters. this testing should work only between 6 PM to 7 PM.**


import java.time.*;
import java.util.*;

class Product {
    String name;
    int price;

    Product(String name, int price) {
        this.name = name;
        this.price = price;
    }
}

public class ShoppingCartSimulation {
    public static void main(String[] args) {
        // Time restriction: only 6PM–7PM
        LocalTime start = LocalTime.of(18, 0); // 6:00 PM
        LocalTime end = LocalTime.of(19, 0);   // 7:00 PM
        LocalTime now = LocalTime.now();

        if (now.isBefore(start) || !now.isBefore(end)) {
            System.out.println("[SKIPPED] Test runs only between 6PM and 7PM. Current time: " + now);
            return;
        }

        // Simulate products being added to cart
        List<Product> cart = new ArrayList<>();
        cart.add(new Product("Laptop", 1500));
        cart.add(new Product("Headphones", 900));
        cart.add(new Product("Keyboard", 300));

        // Calculate total price
        int total = cart.stream().mapToInt(p -> p.price).sum();

        // User name check
        String userName = "UserName10"; // <-- Try changing this
        boolean validUser = userName.matches("^[A-Za-z0-9]{10}$");

        // Display cart details
        System.out.println("=== CART DETAILS ===");
        for (Product p : cart) {
            System.out.println(p.name + " - ₹" + p.price);
        }
        System.out.println("Total Price: ₹" + total);
        System.out.println("User Name: " + userName);
        System.out.println("User Valid? " + validUser);

        // Validate conditions
        if (total > 2000 && validUser) {
            System.out.println("✅ Test Passed: Cart total > 2000 and Username valid");
        } else {
            System.out.println("❌ Test Failed: Conditions not met");
        }
    }
}


**5.Test the login functionality and validate whether user profile details are displayed correctly if the user profile name should not contain following characters (A, C, G, I, L, K) and this testing should work between 12 PM to 3 PM.**


import java.time.*;

public class LoginProfileTest {
    public static void main(String[] args) {
        // Time restriction: test only between 12 PM and 3 PM
        LocalTime start = LocalTime.of(12, 0);
        LocalTime end = LocalTime.of(15, 0);
        LocalTime now = LocalTime.now();

        if (now.isBefore(start) || !now.isBefore(end)) {
            System.out.println("[SKIPPED] Test runs only between 12 PM and 3 PM. Current time: " + now);
            return;
        }

        // Simulated login credentials
        String username = "TestUser";
        String password = "password123";

        // Simulate login
        boolean loginSuccess = login(username, password);

        if (!loginSuccess) {
            System.out.println("❌ Login failed. Test stopped.");
            return;
        }

        // Simulated user profile after login
        String profileName = "DemoUserX"; // <-- change this to test different names
        boolean profileDisplayed = true;  // assume profile loads

        System.out.println("=== LOGIN TEST ===");
        System.out.println("Username: " + username);
        System.out.println("Login Successful? " + loginSuccess);
        System.out.println("Profile Displayed? " + profileDisplayed);
        System.out.println("Profile Name: " + profileName);

        // Validate profile name
        boolean validProfile = validateProfileName(profileName);

        if (profileDisplayed && validProfile) {
            System.out.println("✅ Test Passed: Profile displayed & valid name");
        } else {
            System.out.println("❌ Test Failed: Invalid profile name");
        }
    }

    // Fake login function
    private static boolean login(String user, String pass) {
        return user.equals("TestUser") && pass.equals("password123");
    }

    // Profile name validation (must NOT contain A, C, G, I, L, K)
    private static boolean validateProfileName(String name) {
        return !name.toUpperCase().matches(".*[ACGILK].*");
    }
}




**How to Run**
**1. Open [JDoodle Java Compiler](https://www.jdoodle.com/online-java-compiler/).**
**2. Paste this code → Run.**







  
