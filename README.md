import java.util.Scanner;

public class D_smailPaymentApp {

    // Klas ki reprezante yon itilizatè
    static class User {
        String username;
        String password;
        boolean loggedIn;
        double balance;

        User(String username, String password) {
            this.username = username;
            this.password = password;
            this.loggedIn = false;
            this.balance = 0.0;
        }
    }

    // Klas ki reprezante yon peman MonCash
    static class MoncashPayment {
        double amount;

        MoncashPayment(double amount) {
            this.amount = amount;
        }

        boolean processPayment(User user) {
            if (user.loggedIn && user.balance >= amount) {
                user.balance -= amount;
                return true;
            } else {
                return false;
            }
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        User currentUser = null;
        boolean running = true;

        while (running) {
            System.out.println("---- D_smail Payment ----");
            System.out.println("1. Enskri");
            System.out.println("2. Konekte");
            System.out.println("3. Peman Netflix");
            System.out.println("4. Sòti");
            System.out.println("-------------------------");
            System.out.print("Chwazi yon opsyon: ");
            int choice = scanner.nextInt();
            scanner.nextLine(); // Netwaye buffer lan aprè li li yon nimewo

            switch (choice) {
                case 1:
                    System.out.print("Antre non itilizatè: ");
                    String username = scanner.nextLine();
                    System.out.print("Antre modpas: ");
                    String password = scanner.nextLine();
                    currentUser = new User(username, password);
                    System.out.println("Enskripsyon fet avèk siksè.");
                    break;
                case 2:
                    if (currentUser == null) {
                        System.out.println("Ou pa anrejistre ankò. Tanpri enskri premye.");
                    } else {
                        System.out.print("Antre modpas: ");
                        String enteredPassword = scanner.nextLine();
                        if (enteredPassword.equals(currentUser.password)) {
                            currentUser.loggedIn = true;
                            System.out.println("You konekte.");
                        } else {
                            System.out.println("Modpas la pa kòrèk.");
                        }
                    }
                    break;
                case 3:
                    if (currentUser == null || !currentUser.loggedIn) {
                        System.out.println("Ou dwe konekte anvan ou ka fè peman.");
                    } else {
                        System.out.print("Antre montan pou peman Netflix: ");
                        double paymentAmount = scanner.nextDouble();
                        MoncashPayment payment = new MoncashPayment(paymentAmount);
                        if (payment.processPayment(currentUser)) {
                            System.out.println("Peman fet avèk siksè.");
                        } else {
                            System.out.println("Peman pa tande. Asire w ke ou konekte ak yon kòmantè ekilib.");
                        }
                    }
                    break;
                case 4:
                    running = false;
                    System.out.println("Mèsi! Orevwa.");
                    break;
                default:
                    System.out.println("Opsiyon entwòdi. Tanpri chwazi yon nimewo korèk.");
                    break;
            }
        }

        scanner.close();
    }
}
```

