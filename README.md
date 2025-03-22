import java.util.ArrayList;
import java.util.Scanner;

class Room {
    int roomNumber;
    String type;
    boolean isBooked;
    String guestName;

    public Room(int roomNumber, String type) {
        this.roomNumber = roomNumber;
        this.type = type;
        this.isBooked = false;
        this.guestName = "";
    }
}

class Guest {
    String name;
    String contact;

    public Guest(String name, String contact) {
        this.name = name;
        this.contact = contact;
    }
}

public class HotelBookingSystem {
    static ArrayList<Room> rooms = new ArrayList<>();
    static ArrayList<Guest> guests = new ArrayList<>();
    static Scanner scanner = new Scanner(System.in);

    public static void main(String[] args) {
        initializeRooms();
        
        while (true) {
            System.out.println("\nHotel Booking System");
            System.out.println("1. View Available Rooms");
            System.out.println("2. Book a Room");
            System.out.println("3. Check Out");
            System.out.println("4. View All Guests");
            System.out.println("5. Exit");
            System.out.print("Enter choice: ");
            int choice = scanner.nextInt();
            scanner.nextLine();
            
            switch (choice) {
                case 1:
                    viewAvailableRooms();
                    break;
                case 2:
                    bookRoom();
                    break;
                case 3:
                    checkOut();
                    break;
                case 4:
                    viewGuests();
                    break;
                case 5:
                    System.out.println("Exiting...");
                    return;
                default:
                    System.out.println("Invalid choice. Try again.");
            }
        }
    }

    static void initializeRooms() {
        rooms.add(new Room(101, "Single"));
        rooms.add(new Room(102, "Double"));
        rooms.add(new Room(103, "Suite"));
        rooms.add(new Room(104, "Single"));
        rooms.add(new Room(105, "Double"));
    }

    static void viewAvailableRooms() {
        boolean found = false;
        for (Room room : rooms) {
            if (!room.isBooked) {
                System.out.println("Room Number: " + room.roomNumber + ", Type: " + room.type);
                found = true;
            }
        }
        if (!found) {
            System.out.println("No rooms available.");
        }
    }

    static void bookRoom() {
        System.out.print("Enter Room Number to Book: ");
        int roomNumber = scanner.nextInt();
        scanner.nextLine();
        System.out.print("Enter Guest Name: ");
        String name = scanner.nextLine();
        System.out.print("Enter Guest Contact: ");
        String contact = scanner.nextLine();
        
        for (Room room : rooms) {
            if (room.roomNumber == roomNumber && !room.isBooked) {
                room.isBooked = true;
                room.guestName = name;
                guests.add(new Guest(name, contact));
                System.out.println("Room " + roomNumber + " booked successfully for " + name);
                return;
            }
        }
        System.out.println("Room is either not available or already booked.");
    }

    static void checkOut() {
        System.out.print("Enter Room Number to Check Out: ");
        int roomNumber = scanner.nextInt();
        
        for (Room room : rooms) {
            if (room.roomNumber == roomNumber && room.isBooked) {
                System.out.println("Guest " + room.guestName + " has checked out from Room " + roomNumber);
                room.isBooked = false;
                room.guestName = "";
                return;
            }
        }
        System.out.println("Invalid Room Number or Room is already available.");
    }

    static void viewGuests() {
        if (guests.isEmpty()) {
            System.out.println("No guests currently registered.");
        } else {
            for (Guest guest : guests) {
                System.out.println("Name: " + guest.name + ", Contact: " + guest.contact);
            }
        }
    }
}
