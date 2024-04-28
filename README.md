# library-Management
import java.util.ArrayList;
import java.util.Date;
import java.util.List;

class Book {
    private String title;
    private String author;
    private String isbn;
    private boolean available;

    public Book(String title, String author, String isbn) {
        this.title = title;
        this.author = author;
        this.isbn = isbn;
        this.available = true;
    }

    // Getters and setters
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
        return available;
    }

    public void setAvailable(boolean available) {
        this.available = available;
    }
}

class Patron {
    private String name;
    private int id;

    public Patron(String name, int id) {
        this.name = name;
        this.id = id;
    }

    // Getters
    public String getName() {
        return name;
    }

    public int getId() {
        return id;
    }
}

class BorrowingRecord {
    private Book book;
    private Patron patron;
    private Date borrowDate;
    private Date returnDate;

    public BorrowingRecord(Book book, Patron patron, Date borrowDate) {
        this.book = book;
        this.patron = patron;
        this.borrowDate = borrowDate;
    }

    // Getters and setters
    public Book getBook() {
        return book;
    }

    public Patron getPatron() {
        return patron;
    }

    public Date getBorrowDate() {
        return borrowDate;
    }

    public Date getReturnDate() {
        return returnDate;
    }

    public void setReturnDate(Date returnDate) {
        this.returnDate = returnDate;
    }
}

class Library {
    private List<Book> books;
    private List<Patron> patrons;
    private List<BorrowingRecord> borrowingRecords;

    public Library() {
        books = new ArrayList<>();
        patrons = new ArrayList<>();
        borrowingRecords = new ArrayList<>();
    }

    // Methods to add books, patrons, and record borrowings

    public void addBook(Book book) {
        books.add(book);
    }

    public void addPatron(Patron patron) {
        patrons.add(patron);
    }

    public void borrowBook(Book book, Patron patron, Date borrowDate) {
        if (!book.isAvailable()) {
            System.out.println("This book is not available for borrowing.");
            return;
        }

        book.setAvailable(false);
        borrowingRecords.add(new BorrowingRecord(book, patron, borrowDate));
        System.out.println("Book borrowed successfully.");
    }

    // Other methods for returning books, checking borrowing history, etc.
}

public class Main {
    public static void main(String[] args) {
        Library library = new Library();

        // Adding books to the library
        Book book1 = new Book("Java Programming", "John Smith", "978-0134685991");
        Book book2 = new Book("Data Structures and Algorithms", "Jane Doe", "978-0262533058");
        library.addBook(book1);
        library.addBook(book2);

        // Adding patrons to the library
        Patron patron1 = new Patron("Alice", 1);
        Patron patron2 = new Patron("Bob", 2);
        library.addPatron(patron1);
        library.addPatron(patron2);

        // Borrowing a book
        library.borrowBook(book1, patron1, new Date());

        // Attempting to borrow the same book again
        library.borrowBook(book1, patron2, new Date());
    }
}
