# EXAMEN

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

public class MatrixCalculator {
    public static void main(String[] args) {
        String inputMatrixAFile = "matrixA.txt";
        String inputMatrixCFile = "matrixC.txt";
        String outputMatrixBFile = "matrixB.txt";

        try {
            // Leer matrices A y C desde los archivos
            int[][] matrixA = readMatrixFromFile(inputMatrixAFile);
            int[][] matrixC = readMatrixFromFile(inputMatrixCFile);

            
            int[][] matrixB = calculateMatrixB(matrixA, matrixC);

            writeMatrixToFile(matrixB, outputMatrixBFile);

            System.out.println("Matriz B calculada y guardada en el archivo " + outputMatrixBFile);
        } catch (IOException e) {
            System.out.println("Error al procesar los archivos de matriz: " + e.getMessage());
        }
    }

    private static int[][] readMatrixFromFile(String fileName) throws IOException {
        BufferedReader reader = new BufferedReader(new FileReader(fileName));

        String line;
        int rowCount = 0;
        int columnCount = 0;

        // Obtener el tamaño de la matriz
        while ((line = reader.readLine()) != null) {
            String[] numbers = line.split(" ");
            columnCount = numbers.length;
            rowCount++;
        }

        
        reader.close();
        reader = new BufferedReader(new FileReader(fileName));

        int[][] matrix = new int[rowCount][columnCount];
        int row = 0;

  
        while ((line = reader.readLine()) != null) {
            String[] numbers = line.split(" ");
            for (int col = 0; col < columnCount; col++) {
                matrix[row][col] = Integer.parseInt(numbers[col]);
            }
            row++;
        }

        reader.close();
        return matrix;
    }

    private static int[][] calculateMatrixB(int[][] matrixA, int[][] matrixC) {
        int rowCount = matrixA.length;
        int columnCount = matrixA[0].length;
        int[][] matrixB = new int[rowCount][columnCount];
        
        for (int row = 0; row < rowCount; row++) {
            for (int col = 0; col < columnCount; col++) {
                matrixB[row][col] = matrixC[row][col] - matrixA[row][col];
            }
        }

        return matrixB;
    }

    private static void writeMatrixToFile(int[][] matrix, String fileName) throws IOException {
        BufferedWriter writer = new BufferedWriter(new FileWriter(fileName));

        for (int[] row : matrix) {
            for (int col = 0; col < row.length; col++) {
                writer.write(String.valueOf(row[col]));
                if (col < row.length - 1) {
                    writer.write(" ");
                }
            }
            writer.newLine();
        }

        writer.close();
    }
}
