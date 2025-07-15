package RouletteGame;

import java.util.Random;
import java.util.Scanner;

public class RouletteGame {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Random random = new Random();
        
        double balance = 1000.0;  // Starting balance
        System.out.println("Welcome to the Roulette Game!");
        System.out.println("You start with a balance of $" + balance);
        System.out.println("Press 'Enter' to spin the wheel...");

        // Loop to keep playing until the user exits
        while (true) {
            System.out.println("Your current balance: $" + balance);
            System.out.print("Enter the amount you'd like to bet (or type 'exit' to quit): ");
            String input = scanner.nextLine();
            
            // Exit the game if user types "exit"
            if (input.equalsIgnoreCase("exit")) {
                System.out.println("Thank you for playing! Your final balance is $" + balance);
                break;
            }
            
            // Check if the input is a valid number for the bet
            double betAmount;
            try {
                betAmount = Double.parseDouble(input);
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a valid amount.");
                continue;
            }

            // Check if the bet is within the available balance
            if (betAmount <= 0 || betAmount > balance) {
                System.out.println("Invalid bet amount. Please bet within your current balance.");
                continue;
            }

            // Ask the player to choose a number to bet on (0-36)
            System.out.print("Enter the number you want to bet on (0-36): ");
            int betNumber;
            try {
                betNumber = Integer.parseInt(scanner.nextLine());
                if (betNumber < 0 || betNumber > 36) {
                    System.out.println("Invalid number. Please choose a number between 0 and 36.");
                    continue;
                }
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a valid number.");
                continue;
            }

            // Generate three random numbers (roulette spin)
            int firstSpin = random.nextInt(37);  // 0 to 36
            int secondSpin = random.nextInt(37); // 0 to 36
            int thirdSpin = random.nextInt(37);  // 0 to 36
            
            // Display the results of the spin
            System.out.println("The roulette wheel spins...");
            System.out.println("Results: " + firstSpin + " | " + secondSpin + " | " + thirdSpin);

            // Check if the player won
            if (firstSpin == betNumber || secondSpin == betNumber || thirdSpin == betNumber) {
                // The player won, add a $10,000 prize
                System.out.println("Congratulations! You win $10,000!");
                balance += 10000;  // Add prize to balance
            } else {
                // The player lost, deduct the bet amount
                System.out.println("Sorry, you lost your bet.");
                balance -= betAmount;  // Deduct the bet amount from the balance
            }

            // Check if the balance is zero or negative
            if (balance <= 0) {
                System.out.println("Your balance is zero. Game over!");
                break;
            }

            System.out.println("Your current balance: $" + balance);
            System.out.println("Press 'Enter' to spin again, or type 'exit' to quit.");
            input = scanner.nextLine();
            
            if (input.equalsIgnoreCase("exit")) {
                System.out.println("Thank you for playing! Your final balance is $" + balance);
                break;
            }
        }

        scanner.close();  // Close the scanner when done
    }
    
}
