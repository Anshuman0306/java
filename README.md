import java.util.Scanner;

public class ATM {
    private double balance;
    private String username;
    private String password;

    public ATM(String username, String password) {
        this.username = username;
        this.password = password;
        this.balance = 1000.0; // Initial balance for demonstration purposes
    }

    public boolean authenticate(String enteredUsername, String enteredPassword) {
        return this.username.equals(enteredUsername) && this.password.equals(enteredPassword);
    }

    public void checkBalance() {
        System.out.println("Your balance is: $" + balance);
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawn: $" + amount);
        } else {
            System.out.println("Insufficient funds or invalid amount.");
        }
    }

    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: $" + amount);
        } else {
            System.out.println("Invalid deposit amount.");
        }
    }

    public static void main(String[] args) {
        ATM atm = new ATM("yourUsername", "yourPassword");
        Scanner scanner = new Scanner(System.in);

        System.out.println("Welcome to the ATM.");
        System.out.print("Enter username: ");
        String enteredUsername = scanner.nextLine();

        System.out.print("Enter password: ");
        String enteredPassword = scanner.nextLine();

        if (atm.authenticate(enteredUsername, enteredPassword)) {
            int choice;
            do {
                System.out.println("\n1. Check Balance");
                System.out.println("2. Withdraw");
                System.out.println("3. Deposit");
                System.out.println("4. Exit");
                System.out.print("Enter your choice: ");
                choice = scanner.nextInt();

                switch (choice) {
                    case 1:
                        atm.checkBalance();
                        break;
                    case 2:
                        System.out.print("Enter amount to withdraw: $");
                        double withdrawAmount = scanner.nextDouble();
                        atm.withdraw(withdrawAmount);
                        break;
                    case 3:
                        System.out.print("Enter amount to deposit: $");
                        double depositAmount = scanner.nextDouble();
                        atm.deposit(depositAmount);
                        break;
                    case 4:
                        System.out.println("Thank you for using the ATM. Goodbye!");
                        break;
                    default:
                        System.out.println("Invalid choice. Please enter again.");
                        break;
                }
            } while (choice != 4);
        } else {
            System.out.println("Invalid username or password. Exiting...");
        }
        scanner.close();
    }
}
