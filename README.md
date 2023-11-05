# Week11
Tugas Artificial Intelligent and Aplication Week 11
Nama  : Almas DIqya Wafa'
NIM   : 5311421005
Prodi : Teknik Elektro

Program 1:

package TicTacToe;
/**
 * Enumeration for the various game states of the Tic-Tac-Toe game
 */
public enum State {
    PLAYING, DRAW, CROSS_WON, NOUGHT_WON
}


Penjelasan Program 1:
1. "PLAYING": adalah status permainan saat permainan masih berlangsung, dan tidak ada pemenang atau seri (draw) yang terjadi.
2. "DRAW": Status yang menunjukkan bahwa permainan telah berakhir dengan hasil seri (semua sel pada papan sudah terisi tanpa adanya pemenang).
3. "CROSS_WON": Status yang menunjukkan bahwa pemain yang memainkan tanda "X" telah memenangkan permainan dengan mengisi garis horizontal, vertikal, atau diagonal dengan simbol "X".
4. "NOUGHT_WON": Status yang menunjukkan bahwa pemain yang memainkan tanda "O" telah memenangkan permainan dengan mengisi garis horizontal, vertikal, atau diagonal dengan simbol "O".

Enum "State" digunakan untuk memudahkan pemrogram dalam melacak status permainan saat mengembangkan permainan Tic-Tac-Toe. Dengan menggunakan enum ini, kita dapat dengan mudah mengidentifikasi apakah permainan masih berlangsung, berakhir dengan seri, atau ada pemenangnya.

Program 2:

package TicTacToe;
/**
 * Enumeration for the seeds and cell contents
 */
public enum Seed {
    EMPTY, CROSS, NOUGHT
}

Penjelasan Program 2:
1. "EMPTY" : digunakan untuk merepresentasikan sel kosong atau belum diisi oleh pemain mana pun.
2. "CROSS" : digunakan untuk merepresentasikan sel yang diisi oleh pemain dengan simbol "X".
3. "NOUGHT": digunakan untuk merepresentasikan sel yang diisi oleh pemain dengan simbol "O".

Dengan menggunakan enum "Seed", kita dapat mengidentifikasi isi setiap sel pada papan permainan. 

Program 3:

package TicTacToe;
/**
 * Enumeration for the various states of the game
 */
public enum GameState {
    PLAYING, DRAW, CROSS_WON, NOUGHT_WON
}

Penjelasan Program 3:
1. "PLAYING": adalah status permainan saat permainan masih berlangsung, dan tidak ada pemenang atau seri (draw) yang terjadi.
2. "DRAW": Status yang menunjukkan bahwa permainan telah berakhir dengan hasil seri (semua sel pada papan sudah terisi tanpa adanya pemenang).
3. "CROSS_WON": Status yang menunjukkan bahwa pemain yang memainkan tanda "X" telah memenangkan permainan dengan mengisi garis horizontal, vertikal, atau diagonal dengan simbol "X".
4. "NOUGHT_WON": Status yang menunjukkan bahwa pemain yang memainkan tanda "O" telah memenangkan permainan dengan mengisi garis horizontal, vertikal, atau diagonal dengan simbol "O".

Enum "GameState" digunakan untuk memudahkan pemrogram dalam melacak status permainan saat mengembangkan permainan Tic-Tac-Toe. Dengan menggunakan enum ini, kita dapat dengan mudah mengidentifikasi apakah permainan masih berlangsung, berakhir dengan seri, atau ada pemenangnya.

Program 4:

package TicTacToe;
import java.awt.*;
import java.awt.Graphics;
import java.awt.Graphics2D;

public class Cell {
    // Content of this cell (Seed.EMPTY, Seed.CROSS, or Seed.NOUGHT)
    Seed content;
    int row, col; // Row and column of this cell
    /**
     * Constructor to initialize this cell with the specified row and col
     */
    public Cell(int row, int col) {
        this.row = row;
        this.col = col;
        clear(); // Clear content
    }
    /**
     * Clear this cell's content to EMPTY
     */
    public void clear() {
        content = Seed.EMPTY;
    }
    /**
     * Paint itself on the graphics canvas, given the Graphics context
     */
    public void paint(Graphics g) {
        // Use Graphics2D which allows us to set the pen's stroke
        Graphics2D g2d = (Graphics2D) g;
        g2d.setStroke(new BasicStroke(GameMain.SYMBOL_STROKE_WIDTH, BasicStroke.CAP_ROUND, BasicStroke.JOIN_ROUND)); // Graphics2D only
        // Draw the Seed if it is not empty
        int x1 = col * GameMain.CELL_SIZE + GameMain.CELL_PADDING;
        int y1 = row * GameMain.CELL_SIZE + GameMain.CELL_PADDING;
        if (content == Seed.CROSS) {
            g2d.setColor(Color.RED);
            int x2 = (col + 1) * GameMain.CELL_SIZE - GameMain.CELL_PADDING;
            int y2 = (row + 1) * GameMain.CELL_SIZE - GameMain.CELL_PADDING;
            g2d.drawLine(x1, y1, x2, y2);
            g2d.drawLine(x2, y1, x1, y2);
        } else if (content == Seed.NOUGHT) {
            g2d.setColor(Color.BLUE);
            g2d.drawOval(x1, y1, GameMain.SYMBOL_SIZE, GameMain.SYMBOL_SIZE);
        }
    }
}

Penjelasan Program 4:
Program yang ada pada kelas "Cell" digunakan untuk merepresentasikan sel pada papan permainan Tic-Tac-Toe dan menggambar isi sel tersebut berdasarkan tipe "Seed" yang diatur dalam "content".
  a. "Seed content" : Variabel ini digunakan untuk menyimpan isi sel, yang dapat berupa "Seed.EMPTY", "Seed.CROSS", atau "Seed.NOUGHT".
  b. "int row, col"c: Variabel ini digunakan untuk menyimpan baris (row) dan kolom (column) di mana sel berada.
  c. "Cell(int row, int col)" : Ini adalah konstruktor yang digunakan untuk menginisialisasi objek "Cell" dengan baris dan kolom yang sesuai. Pada awalnya, isi sel diatur ke "Seed.EMPTY" dengan memanggil metode "clear()".
  d. "clear()" : Metode ini digunakan untuk mengosongkan isi sel dengan mengatur "content" ke "Seed.EMPTY".
  e. "paint(Graphics g)" : Metode ini digunakan untuk menggambar sel pada canvas grafis. Ini menggunakan objek "Graphics2D" untuk mengontrol stroke (tebal garis) dan menggambar simbol "X" atau lingkaran "O" sesuai dengan isi sel. Juga, warna yang digunakan adalah merah untuk "X" dan biru untuk "O".

Program 5:

package TicTacToe;
import java.awt.*;
/**
 * The Board class models the ROWS-by-COLS game-board.
 */
public class Board {
    // Package access
    // Composes of a 2D array of ROWS-by-COLS Cell instances
    Cell[][] cells;

    /** Constructor to initialize the game board */
    public Board() {
        // Allocate the array
        cells = new Cell[GameMain.ROWS][GameMain.COLS];
        for (int row = 0; row < GameMain.ROWS; ++row) {
            for (int col = 0; col < GameMain.COLS; ++col) {
                // Allocate element of the array
                cells[row][col] = new Cell(row, col);
            }
        }
    }

    /** Initialize (or re-initialize) the game board */
    public void init() {
        for (int row = 0; row < GameMain.ROWS; ++row) {
            for (int col = 0; col < GameMain.COLS; ++col) {
                // Clear the cell content
                cells[row][col].clear();
            }
        }
    }

    /** Return true if it is a draw (i.e., no more EMPTY cell) */
    public boolean isDraw() {
        for (int row = 0; row < GameMain.ROWS; ++row) {
            for (int col = 0; col < GameMain.COLS; ++col) {
                if (cells[row][col].content == Seed.EMPTY) {
                    // An empty seed found, not a draw, exit
                    return false;
                }
            }
        }
        return true; // No empty cell, it's a draw
    }

    /** Return true if the player with "seed" has won after placing at (seedRow, seedCol) */
    public boolean hasWon(Seed seed, int seedRow, int seedCol) {
        return (cells[seedRow][0].content == seed && // 3-in-a-row
                cells[seedRow][1].content == seed &&
                cells[seedRow][2].content == seed
                || cells[0][seedCol].content == seed && // 3-in-a-column
                cells[1][seedCol].content == seed &&
                cells[2][seedCol].content == seed
                || seedRow == seedCol && // 3-in-a-diagonal
                cells[0][0].content == seed &&
                cells[1][1].content == seed &&
                cells[2][2].content == seed
                || seedRow + seedCol == 2 && // 3-in-the-opposite-diagonal
                cells[0][2].content == seed &&
                cells[1][1].content == seed &&
                cells[2][0].content == seed);
    }

    /** Paint itself on the graphics canvas, given the Graphics context */
    public void paint(Graphics g) {
        // Draw the grid-lines
        g.setColor(Color.GRAY);
        for (int row = 1; row < GameMain.ROWS; ++row) {
            g.fillRoundRect(0, GameMain.CELL_SIZE * row - GameMain.GRID_WIDTH_HALF,
                    GameMain.CANVAS_WIDTH - 1, GameMain.GRID_WIDTH, GameMain.GRID_WIDTH, GameMain.GRID_WIDTH);
        }
        for (int col = 1; col < GameMain.COLS; ++col) {
            g.fillRoundRect(GameMain.CELL_SIZE * col - GameMain.GRID_WIDTH_HALF, 0,
                    GameMain.GRID_WIDTH, GameMain.CANVAS_HEIGHT - 1, GameMain.GRID_WIDTH, GameMain.GRID_WIDTH);
        }
        // Draw all the cells
        for (int row = 0; row < GameMain.ROWS; ++row) {
            for (int col = 0; col < GameMain.COLS; ++col) {
                cells[row][col].paint(g); // Ask the cell to paint itself
            }
        }
    }
}

Penjelasan Program 5:
Program yang pada kelas "Board" digunakan untuk mengelola papan permainan Tic-Tac-Toe dan menggambar papan permainan serta sel-selnya saat permainan berlangsung. Program ini juga memiliki metode untuk menginisialisasi papan, memeriksa apakah terdapat seri (draw) dalam permainan, dan untuk memeriksa apakah pemain dengan simbol "X" atau "O" telah memenangkan permainan.
  a. "Cell[][] cells" : Variabel ini adalah 2D array yang merepresentasikan sel-sel pada papan permainan.
  b. "Board()" : Konstruktor ini digunakan untuk menginisialisasi objek "Board" dengan membuat sel-sel pada papan permainan menggunakan objek "Cell" dan mengatur kontennya sebagai "Seed.EMPTY".
  c. "init()" : Metode ini digunakan untuk menginisialisasi ulang papan permainan dengan mengosongkan semua sel-selnya.
  d. "isDraw()" : Metode ini memeriksa apakah terdapat seri (draw) dalam permainan dengan memeriksa apakah sel-sel di papan telah diisi semua atau tidak.
  e. "hasWon(Seed seed, int seedRow, int seedCol)" : Metode ini digunakan untuk memeriksa apakah pemain dengan simbol "seed" (biasanya "X" atau "O") telah memenangkan permainan setelah menempatkan tanda pada sel yang terletak di "seedRow" dan "seedCol". Ini memeriksa kondisi-kondisi berbeda (3-in-a-row, 3-in-a-column, 3-in-a-diagonal, dan 3-in-the-opposite-diagonal) untuk menentukan pemenang.
  f. "paint(Graphics g)" : Metode ini digunakan untuk menggambar papan permainan dan sel-selnya pada canvas grafis. Ini juga menggambar garis-garis pembatas antar sel pada papan.

Program 6:

package TicTacToe;
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

@SuppressWarnings("serial")
public class GameMain extends JPanel {
    public static final int ROWS = 3;
    public static final int COLS = 3;
    public static final String TITLE = "Tic Tac Toe";
    public static final int CELL_SIZE = 100;
    public static final int CANVAS_WIDTH = CELL_SIZE * COLS;
    public static final int CANVAS_HEIGHT = CELL_SIZE * ROWS;
    public static final int GRID_WIDTH = 8;
    public static final int GRID_WIDTH_HALF = GRID_WIDTH / 2;
    public static final int CELL_PADDING = CELL_SIZE / 6;
    public static final int SYMBOL_SIZE = CELL_SIZE - CELL_PADDING * 2;
    public static final int SYMBOL_STROKE_WIDTH = 8;
    private Board board;
    private GameState currentState;
    private Seed currentPlayer;
    private JLabel statusBar;
    public GameMain() {
        this.addMouseListener(new MouseAdapter() {
            @Override
            public void mouseClicked(MouseEvent e) {
                int mouseX = e.getX();
                int mouseY = e.getY();
                int rowSelected = mouseY / CELL_SIZE;
                int colSelected = mouseX / CELL_SIZE;
                if (currentState == GameState.PLAYING) {
                    if (rowSelected >= 0 && rowSelected < ROWS
                            && colSelected >= 0 && colSelected < COLS
                            && board.cells[rowSelected][colSelected].content == Seed.EMPTY) {
                        board.cells[rowSelected][colSelected].content = currentPlayer;
                        updateGame(currentPlayer, rowSelected, colSelected);
                        currentPlayer = (currentPlayer == Seed.CROSS) ? Seed.NOUGHT : Seed.CROSS;
                    }
                } else {
                    initGame();
                }
                repaint();
            }
        });
        statusBar = new JLabel(" ");
        statusBar.setFont(new Font(Font.DIALOG_INPUT, Font.BOLD, 14));
        statusBar.setBorder(BorderFactory.createEmptyBorder(2, 5, 4, 5));
        statusBar.setOpaque(true);
        statusBar.setBackground(Color.LIGHT_GRAY);
        setLayout(new BorderLayout());
        add(statusBar, BorderLayout.PAGE_END);
        setPreferredSize(new Dimension(CANVAS_WIDTH, CANVAS_HEIGHT + 30));
        board = new Board();
        initGame();
    }
    public void initGame() {
        for (int row = 0; row < ROWS; ++row) {
            for (int col = 0; col < COLS; ++col) {
                board.cells[row][col].content = Seed.EMPTY;
            }
        }
        currentState = GameState.PLAYING;
        currentPlayer = Seed.CROSS;
    }
    public void updateGame(Seed theSeed, int row, int col) {
        if (board.hasWon(theSeed, row, col)) {
            currentState = (theSeed == Seed.CROSS) ? GameState.CROSS_WON : GameState.NOUGHT_WON;
        } else if (board.isDraw()) {
            currentState = GameState.DRAW;
        }
    }
    @Override
    public void paintComponent(Graphics g) {
        super.paintComponent(g);
        setBackground(Color.WHITE);
        board.paint(g);
        if (currentState == GameState.PLAYING) {
            statusBar.setForeground(Color.BLACK);
            if (currentPlayer == Seed.CROSS) {
                statusBar.setText("X's Turn");
            } else {
                statusBar.setText("O's Turn");
            }
        } else if (currentState == GameState.DRAW) {
            statusBar.setForeground(Color.RED);
            statusBar.setText("It's a Draw! Click to play again.");
        } else if (currentState == GameState.CROSS_WON) {
            statusBar.setForeground(Color.RED);
            statusBar.setText("'X' Won! Click to play again.");
        } else if (currentState == GameState.NOUGHT_WON) {
            statusBar.setForeground(Color.RED);
            statusBar.setText("'O' Won! Click to play again.");
        }
    }
    public static void main(String[] args) {
        javax.swing.SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                JFrame frame = new JFrame(TITLE);
                frame.setContentPane(new GameMain());
                frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
                frame.pack();
                frame.setLocationRelativeTo(null);
                frame.setVisible(true);
            }
        });
    }
}

Penjelasan Program 6:
1. Import Package : Program mengimpor beberapa paket yang diperlukan dari Java AWT dan Swing untuk membuat GUI dan mengelola peristiwa (events).
2. Class "GameMain" : Ini adalah kelas utama yang memperluas "JPanel". Ini adalah panel tempat permainan Tic-Tac-Toe akan digambar.
3. Variabel Konstan : Program mendefinisikan beberapa variabel konstan seperti "ROWS", "COLS", "CELL_SIZE", dan sebagainya, yang digunakan untuk mengatur dimensi dan tampilan permainan.
4. Kelas "Board" : Program menciptakan objek "Board" untuk mengatur papan permainan, berisi sel-sel untuk permainan.
5. MouseListener : Program menambahkan "MouseListener" ke panel untuk menangani peristiwa klik mouse oleh pemain. Ini digunakan untuk menentukan langkah pemain, mengupdate permainan, dan menampilkan perubahan pada papan permainan.
6. JLabel "statusBar" : Ini adalah label yang digunakan untuk menampilkan pesan status permainan, seperti giliran pemain, hasil akhir, dan pesan lainnya.
7. "initGame" : Ini adalah metode yang menginisialisasi papan permainan dengan mengosongkan sel-sel dan mengatur pemain yang akan memulai permainan.
8. "updateGame" : Ini adalah metode yang digunakan untuk memeriksa apakah pemain yang saat ini memiliki "theSeed" telah memenangkan permainan atau jika permainan berakhir dengan seri.
9. "paintComponent" : Ini adalah metode yang digunakan untuk menggambar elemen-elemen permainan pada panel. Ini juga menggambarkan papan permainan, mengganti warna latar belakang, dan menampilkan pesan status.
10. "main" Method : Metode ini adalah titik masuk utama ke program. Ini membuat objek JFrame, menambahkan instance dari "GameMain" ke JFrame, mengatur beberapa atribut frame, dan menampilkan frame.

Program ini memungkinkan pemain untuk bermain Tic-Tac-Toe secara bergantian dengan mengklik sel-sel pada papan permainan, dan hasil permainan (siapa yang menang, seri, atau giliran berikutnya) akan ditampilkan di status bar. Program ini dijalankan di dalam sebuah jendela JFrame.

Hasil Percobaan:
1. Tampilan awal ketika program dijalankan, terdapat 6 kotak kosong dan diawali dengan giliran "X" untuk mengisi kotak terlebih dahulu.
   
   ![image](https://github.com/AlmasDiqya22/Week11/assets/148710085/3bac234d-e35e-4f0a-986f-653fe205bd6e)
   
2. Tampilan ketika "X" memenangkan pertandingan.
   
   ![image](https://github.com/AlmasDiqya22/Week11/assets/148710085/43eb108a-cc4a-477b-901a-ea6e43b0d03a)
   
3. Tampilan ketika "O" memenangkan pertandingan.
   
   ![image](https://github.com/AlmasDiqya22/Week11/assets/148710085/3274d95b-5204-41b3-9461-f8b8cf6b6395)
   
4. Tampilan ketika hasil pertandingan seri.
   
   ![image](https://github.com/AlmasDiqya22/Week11/assets/148710085/6bda1a64-5e44-447e-8c7a-b83c664b14d1)

