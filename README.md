import java.util.ArrayList;
import java.util.Scanner;

class Reservation {
    String name;
    String time;
    boolean paid;

    Reservation(String name, String time) {
        this.name = name;
        this.time = time;
        this.paid = false;
    }

    public String toString() {
        return name + " at " + time + (paid ? " [Paid]" : " [Pending Payment]");
    }
}

public class ReservationSystem {
    static ArrayList<Reservation> reservations = new ArrayList<>();
    static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        System.out.println("🤖 Welcome! I can help you make or cancel reservations.");
        System.out.println("Type 'book', 'cancel', 'view', 'pay', 'help' or 'bye' to exit.");

        while (true) {
            System.out.print("\nYou: ");
            String input = scanner.nextLine().trim().toLowerCase();

            switch (input) {
                case "book":
                    makeReservation();
                    break;
                case "cancel":
                    cancelReservation();
                    break;
                case "view":
                    viewReservations();
                    break;
                case "pay":
                    simulatePayment();
                    break;
                case "help":
                    printHelp();
                    break;
                case "bye":
                    System.out.println("Bot: Thank you! Have a nice day. 👋");
                    return;
                default:
                    System.out.println("Bot: Sorry, I didn't understand that. Type 'help' for options.");
            }
        }
    }

    static void makeReservation() {
        System.out.print("Bot: What's your name? ");
        String name = scanner.nextLine();

        System.out.print("Bot: What time would you like to book? ");
        String time = scanner.nextLine();

        Reservation res = new Reservation(name, time);
        reservations.add(res);
        System.out.println("Bot: Reservation made for " + name + " at " + time + ". Payment pending.");
    }

    static void cancelReservation() {
        System.out.print("Bot: Enter your name to cancel reservation: ");
        String name = scanner.nextLine();

        boolean found = false;
        for (Reservation r : reservations) {
            if (r.name.equalsIgnoreCase(name)) {
                reservations.remove(r);
                System.out.println("Bot: Reservation for " + name + " canceled.");
                found = true;
                break;
            }
        }

        if (!found) {
            System.out.println("Bot: No reservation found under that name.");
        }
    }

    static void viewReservations() {
        if (reservations.isEmpty()) {
            System.out.println("Bot: No current reservations.");
        } else {
            System.out.println("Bot: Here are the current reservations:");
            for (Reservation r : reservations) {
                System.out.println(" - " + r);
            }
        }
    }

    static void simulatePayment() {
        System.out.print("Bot: Enter your name to pay for your reservation: ");
        String name = scanner.nextLine();

        boolean found = false;
        for (Reservation r : reservations) {
            if (r.name.equalsIgnoreCase(name)) {
                if (r.paid) {
                    System.out.println("Bot: You've already paid.");
                } else {
                    r.paid = true;
                    System.out.println("Bot: Payment successful for " + r.name + ".");
                }
                found = true;
                break;
            }
        }

        if (!found) {
            System.out.println("Bot: No reservation found under that name.");
        }
    }

    static void printHelp() {
        System.out.println("Bot: Here are the available commands:");
        System.out.println(" - book    : Make a reservation");
        System.out.println(" - cancel  : Cancel an existing reservation");
        System.out.println(" - view    : View all reservations");
        System.out.println(" - pay     : Make a payment");
        System.out.println(" - help    : Show help");
        System.out.println(" - bye     : Exit the chatbot");
    }
}
