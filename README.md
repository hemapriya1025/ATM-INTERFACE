# ATM-INTERFACE
import java.util.Scanner;

// Represents a simple bank account
class Account {
    private double balance;

    public Account(double openingBalance) {
        balance = openingBalance;
    }

    public String addFunds(double amount) {
        if (amount <= 0) return "⚠️ Enter a valid amount to deposit.";
        balance += amount;
        return "✅ Deposited ₹" + amount + " successfully.";
    }

    public String takeOutFunds(double amount) {
        if (amount <= 0) return "⚠️ Invalid withdrawal amount.";
        if (amount > balance) return "❌ Insufficient funds.";
        balance -= amount;
        return "✅ Withdrawn ₹" + amount + ".";
    }

    public String displayBalance() {
        return "💰 Your current balance is: ₹" + balance;
    }
}

// Main ATM application
public class Main {
    private static final Scanner input = new Scanner(System.in);
    private static final Account userAccount = new Account(750);  // Starting with ₹750

    public static void main(String[] args) {
        int option;

        System.out.println("🌟 Welcome to the Digital ATM 🌟");

        do {
            showOptions();
            System.out.print("➡️ Choose an option (1-4): ");
            option = input.nextInt();

            switch (option) {
                case 1 -> handleWithdraw();
                case 2 -> handleDeposit();
                case 3 -> System.out.println(userAccount.displayBalance());
                case 4 -> System.out.println("👋 Session ended. Take care!");
                default -> System.out.println("❌ Invalid selection. Try again.");
            }
        } while (option != 4);
    }

    private static void showOptions() {
        System.out.println("\n======== ATM Menu ========");
        System.out.println("1️⃣ Withdraw Cash");
        System.out.println("2️⃣ Deposit Cash");
        System.out.println("3️⃣ Check Balance");
        System.out.println("4️⃣ Exit");
    }

    private static void handleWithdraw() {
        System.out.print("💵 Enter amount to withdraw: ₹");
        double cashOut = input.nextDouble();
        String result = userAccount.takeOutFunds(cashOut);
        System.out.println(result);
    }

    private static void handleDeposit() {
        System.out.print("💰 Enter amount to deposit: ₹");
        double cashIn = input.nextDouble();
        String result = userAccount.addFunds(cashIn);
        System.out.println(result);
    }
}
