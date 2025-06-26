Book.java
 
public class Book {
    private String title;
    private String author;
    private String isbn;
    private boolean isAvailable;

    public Book(String title, String author, String isbn) {
        this.title = title;
        this.author = author;
        this.isbn = isbn;
        this.isAvailable = true; // Book is available when created
    }

    // Getters and Setters
    public String getTitle() {
        return title;
    }

    public String getAuthor() {
        return author;
    }

    public String getIsbn() {
        return isbn;
    }

    public boolean isAvailable() {
        return isAvailable;
    }

    public void setAvailable(boolean available) {
        isAvailable = available;
    }
}
 

User.java

 
public class User {
    private String name;
    private String userId;

    public User(String name, String userId) {
        this.name = name;
        this.userId = userId;
    }

    // Getters
    public String getName() {
        return name;
    }

    public String getUserId() {
        return userId;
    }
}
 

Library.java

 
import java.util.ArrayList;
import java.util.List;

public class Library {
    private List<Book> books;
    private List<User> users;

    public Library() {
        books = new ArrayList<>();
        users = new ArrayList<>();
    }

    public void addBook(Book book) {
        books.add(book);
    }

    public void addUser(User user) {
        users.add(user);
    }

    public boolean issueBook(String isbn, User user) {
        for (Book book : books) {
            if (book.getIsbn().equals(isbn) && book.isAvailable()) {
                book.setAvailable(false); // Mark book as issued
                System.out.println("Book issued to " + user.getName());
                return true;
            }
        }
        System.out.println("Book not available");
        return false;
    }

    public boolean returnBook(String isbn) {
        for (Book book : books) {
            if (book.getIsbn().equals(isbn) && !book.isAvailable()) {
                book.setAvailable(true); // Mark book as returned
                System.out.println("Book returned");
                return true;
            }
        }
        System.out.println("Book was not issued");
        return false;
    }

    public void listBooks() {
        for (Book book : books) {
            System.out.println(book.getTitle() + " by " + book.getAuthor() + " (ISBN: " + book.getIsbn() + ") - " + (book.isAvailable() ? "Available" : "Issued"));
        }
    }
}
 

LibraryManagementSystem.java

 
public class LibraryManagementSystem {
    public static void main(String[] args) {
        Library library = new Library();

        // Adding some books
        Book book1 = new Book("1984", "George Orwell", "123456789");
        Book book2 = new Book("Brave New World", "Aldous Huxley", "987654321");

        library.addBook(book1);
        library.addBook(book2);

        // Adding a user
        User user1 = new User("Alice", "U001");

        // Issue a book
        library.issueBook("123456789", user1);
        library.listBooks(); // List all books

        // Return a book
        library.returnBook("123456789");
        library.listBooks(); // List all books again
    }
}
 
