# Digital-library-book-management-system

import java.util.*;

class Book {
    private String bookId;
    private String title;
    private String author;
    private String genre;
    private String availabilityStatus;

    // Constructor
    public Book(String bookId, String title, String author, String genre, String availabilityStatus) {
        this.bookId = bookId;
        this.title = title;
        this.author = author;
        this.genre = genre;
        this.availabilityStatus = availabilityStatus;
    }

    // Getters & Setters
    public String getBookId() { return bookId; }
    public String getTitle() { return title; }
    public String getAuthor() { return author; }
    public String getGenre() { return genre; }
    public String getAvailabilityStatus() { return availabilityStatus; }

    public void setTitle(String title) { this.title = title; }
    public void setAuthor(String author) { this.author = author; }
    public void setGenre(String genre) { this.genre = genre; }
    public void setAvailabilityStatus(String status) { this.availabilityStatus = status; }

    @Override
    public String toString() {
        return "Book ID: " + bookId + " | Title: " + title + " | Author: " + author +
               " | Genre: " + genre + " | Status: " + availabilityStatus;
    }
}

class LibrarySystem {
    private List<Book> books = new ArrayList<>();

    // 📌 Add a Book
    public void addBook(String bookId, String title, String author, String genre, String status) {
        if (title.isEmpty() || author.isEmpty()) {
            System.out.println("Error: Title and Author cannot be empty!");
            return;
        }
        for (Book book : books) {
            if (book.getBookId().equals(bookId)) {
                System.out.println("Error: Book ID must be unique!");
                return;
            }
        }
        books.add(new Book(bookId, title, author, genre, status));
        System.out.println("✅ Book added successfully.");
    }

    // 📌 View All Books
    public void viewAllBooks() {
        if (books.isEmpty()) {
            System.out.println("No books available.");
        } else {
            for (Book book : books) {
                System.out.println(book);
            }
        }
    }

    // 📌 Search Book by ID or Title
    public void searchBook(String query) {
        for (Book book : books) {
            if (book.getBookId().equalsIgnoreCase(query) || book.getTitle().equalsIgnoreCase(query)) {
                System.out.println(book);
                return;
            }
        }
        System.out.println("Book not found.");
    }

    // 📌 Update Book Details
    public void updateBook(String bookId, String newTitle, String newAuthor, String newGenre, String newStatus) {
        for (Book book : books) {
            if (book.getBookId().equals(bookId)) {
                book.setTitle(newTitle);
                book.setAuthor(newAuthor);
                book.setGenre(newGenre);
                book.setAvailabilityStatus(newStatus);
                System.out.println("✅ Book updated successfully.");
                return;
            }
        }
        System.out.println("Error: Book not found.");
    }

    // 📌 Delete a Book
    public void deleteBook(String bookId) {
        Iterator<Book> iterator = books.iterator();
        while (iterator.hasNext()) {
            if (iterator.next().getBookId().equals(bookId)) {
                iterator.remove();
                System.out.println("✅ Book deleted successfully.");
                return;
            }
        }
        System.out.println("Error: Book not found.");
    }
}

public class DigitalLibrary {
    public static void main(String[] args) {
        LibrarySystem library = new LibrarySystem();
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("\n📚 Digital Library Management System");
            System.out.println("1️⃣ Add Book");
            System.out.println("2️⃣ View All Books");
            System.out.println("3️⃣ Search Book");
            System.out.println("4️⃣ Update Book");
            System.out.println("5️⃣ Delete Book");
            System.out.println("6️⃣ Exit");
            System.out.print("Select an option: ");

            int choice = scanner.nextInt();
            scanner.nextLine(); // Consume newline

            switch (choice) {
                case 1: // Add Book
                    System.out.print("Enter Book ID: ");
                    String id = scanner.nextLine();
                    System.out.print("Enter Title: ");
                    String title = scanner.nextLine();
                    System.out.print("Enter Author: ");
                    String author = scanner.nextLine();
                    System.out.print("Enter Genre: ");
                    String genre = scanner.nextLine();
                    System.out.print("Enter Availability (Available/Checked Out): ");
                    String status = scanner.nextLine();
                    library.addBook(id, title, author, genre, status);
                    break;

                case 2: // View All Books
                    library.viewAllBooks();
                    break;

                case 3: // Search Book
                    System.out.print("Enter Book ID or Title to search: ");
                    String searchQuery = scanner.nextLine();
                    library.searchBook(searchQuery);
                    break;

                case 4: // Update Book
                    System.out.print("Enter Book ID to update: ");
                    String updateId = scanner.nextLine();
                    System.out.print("Enter New Title: ");
                    String newTitle = scanner.nextLine();
                    System.out.print("Enter New Author: ");
                    String newAuthor = scanner.nextLine();
                    System.out.print("Enter New Genre: ");
                    String newGenre = scanner.nextLine();
                    System.out.print("Enter New Availability (Available/Checked Out): ");
                    String newStatus = scanner.nextLine();
                    library.updateBook(updateId, newTitle, newAuthor, newGenre, newStatus);
                    break;

                case 5: // Delete Book
                    System.out.print("Enter Book ID to delete: ");
                    String deleteId = scanner.nextLine();
                    library.deleteBook(deleteId);
                    break;

                case 6: // Exit
                    System.out.println("📖 Exiting Digital Library System...");
                    scanner.close();
                    System.exit(0);

                default:
                    System.out.println("❌ Invalid choice! Please select a valid option.");
            }
        }
    }
}
