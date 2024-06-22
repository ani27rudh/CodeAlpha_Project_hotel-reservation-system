import java.util.*;

public class HotelReservationSystem {
    private static Scanner scanner = new Scanner(System.in);
    private static Map<Integer, Boolean> roomAvailability = new HashMap<>();
    private static Map<Integer, String> roomBookings = new HashMap<>();

    public static void main(String[] args) {
        initializeRooms();
        String action;
        do {
            System.out.println("Welcome to the Hotel Reservation System");
            System.out.println("1: Check Room Availability");
            System.out.println("2: Make a Reservation");
            System.out.println("3: View Booking Details");
            System.out.println("4: Exit");
            System.out.print("Choose an action: ");
            action = scanner.nextLine();

            switch (action) {
                case "1":
                    checkRoomAvailability();
                    break;
                case "2":
                    makeReservation();
                    break;
                case "3":
                    viewBookingDetails();
                    break;
                case "4":
                    System.out.println("Exiting system...");
                    break;
                default:
                    System.out.println("Invalid option, please try again.");
            }
        } while (!action.equals("4"));
    }

    private static void initializeRooms() {
        // Let's assume the hotel has 10 rooms
        for (int i = 1; i <= 10; i++) {
            roomAvailability.put(i, true); // All rooms are initially available
        }
    }

    private static void checkRoomAvailability() {
        System.out.println("Available Rooms:");
        roomAvailability.forEach((roomNumber, isAvailable) -> {
            if (isAvailable) {
                System.out.println("Room " + roomNumber);
            }
        });
    }

    private static void makeReservation() {
        System.out.print("Enter room number to reserve: ");
        int roomNumber = scanner.nextInt();
        scanner.nextLine(); // Consume newline left-over
        if (roomAvailability.getOrDefault(roomNumber, false)) {
            System.out.print("Enter your name for the booking: ");
            String guestName = scanner.nextLine();
            roomBookings.put(roomNumber, guestName);
            roomAvailability.put(roomNumber, false);
            System.out.println("Reservation made successfully for Room " + roomNumber);
        } else {
            System.out.println("Sorry, that room is not available.");
        }
    }

    private static void viewBookingDetails() {
        System.out.print("Enter your room number: ");
        int roomNumber = scanner.nextInt();
        scanner.nextLine(); // Consume newline left-over
        if (roomBookings.containsKey(roomNumber)) {
            System.out.println("Booking details for Room " + roomNumber + ":");
            System.out.println("Guest Name: " + roomBookings.get(roomNumber));
        } else {
            System.out.println("No booking found for that room.");
        }
    }
}
