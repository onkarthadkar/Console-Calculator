# Console-Calculator
import java.util.Scanner;
import java.io.*;

 class Calculator {
	
	public static void main(String[] args) {
        int choice;
        int x = 0;
        int y = 0;

        try (PrintStream out = new PrintStream("calclog.txt");
             Scanner input = new Scanner(System.in)) {

            do {
                System.out.println("Console Calculator Program");
                System.out.println("-------------------------\n");
                System.out.println("1. Add");
                System.out.println("2. Subtract");
                System.out.println("3. Multiply");
                System.out.println("4. Divide");
                System.out.println("99. End Program\n");
                System.out.print("Enter Choice: ");

                choice = getValidChoice(input);

                if (choice != 99) {
                    System.out.print("Please enter 2 numbers only: ");
                    x = input.nextInt();
                    y = input.nextInt();
                    performOperation(choice, x, y, out);
                }

            } while (choice != 99);

            System.out.println("Ending program...");

        } catch (Exception e) {
            System.out.println("ERROR: Some error occurred");
            e.printStackTrace();
        }
    }

    private static int getValidChoice(Scanner input) {
        int choice;
        while (true) {
            choice = input.nextInt();
            if ((choice >= 1 && choice <= 4) || choice == 99) {
                break;
            }
            System.out.println("Please enter 1, 2, 3, 4, or 99: ");
        }
        return choice;
    }

    private static void performOperation(int choice, int x, int y, PrintStream out) {
        Calculator calc = new Calculator();
        int result;

        switch (choice) {
            case 1:
                result = calc.add(x, y);
                System.out.printf("The sum is %d\n\n", result);
                out.println(x + " + " + y + " = " + result);
                break;
            case 2:
                result = calc.sub(x, y);
                System.out.printf("The difference is %d\n\n", result);
                out.println(x + " - " + y + " = " + result);
                break;
            case 3:
                result = calc.multi(x, y);
                System.out.printf("The product is %d\n\n", result);
                out.println(x + " * " + y + " = " + result);
                break;
            case 4:
                try {
                    result = calc.div(x, y);
                    System.out.printf("The quotient is %d\n\n", result);
                    out.println(x + " / " + y + " = " + result);
                } catch (ArithmeticException e) {
                    System.out.println("\nError: Cannot divide by zero\n\n");
                }
                break;
        }
    }

    public int add(int num1, int num2) {
        return num1 + num2;
    }

    public int sub(int num1, int num2) {
        return num1 - num2;
    }

    public int multi(int num1, int num2) {
        return num1 * num2;
    }

    public int div(int num1, int num2) {
        if (num2 == 0) {
            throw new ArithmeticException("Cannot divide by zero");
        }
        return num1 / num2;
    }
}
	
