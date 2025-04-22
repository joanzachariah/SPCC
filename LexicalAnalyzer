import java.io.*;
import java.util.*;

public class LexicalAnalyzer {
    public static void main(String[] args) {
        List<String> keywords = List.of("if", "else", "while", "for", "do", "switch", "case", "break", "continue",
                "return", "void", "main", "class", "public", "static", "final", "import", "new", "this", "true",
                "false", "null", "int", "float", "double", "char", "string", "then");

        List<String> operators = List.of("=", "+", "-", "*", "/", "%", "++", "--", "&&", "||", "!", "<", ">", "<=", ">=");
        List<String> symbols = List.of("{", "}", "(", ")", "[", "]", ";", ",", ".");

        Set<String> keywordSet = new HashSet<>();
        Set<String> operatorSet = new HashSet<>();
        Set<String> symbolSet = new HashSet<>();
        Set<String> literalSet = new HashSet<>();
        Set<String> identifierSet = new HashSet<>();
        List<String> allWords = new ArrayList<>();

        try (BufferedReader br = new BufferedReader(new FileReader("Source.txt"))) {
            String line;
            while ((line = br.readLine()) != null) {
                Collections.addAll(allWords, line.split("\\s+"));
            }
        } catch (IOException e) {
            System.out.println("Error reading Source.txt: " + e.getMessage());
            return;
        }

        for (String word : allWords) {
            String lw = word.toLowerCase();
            if (keywords.contains(lw)) keywordSet.add(word);
            else if (operators.contains(word)) operatorSet.add(word);
            else if (symbols.contains(word)) symbolSet.add(word);
            else if (word.matches("\\d+(\\.\\d+)?")) literalSet.add(word);
            else identifierSet.add(word);
        }

        System.out.println("Keywords: " + keywordSet);
        System.out.println("Operators: " + operatorSet);
        System.out.println("Symbols: " + symbolSet);
        System.out.println("Literals: " + literalSet);
        System.out.println("Identifiers: " + identifierSet);

        System.out.println("\nSymbol Table:\n---------------------------");
        System.out.println("Lexeme\t\tToken\n---------------------------");

        Map<String, Integer> idMap = new HashMap<>();
        int id = 1;
        for (String word : allWords) {
            String lw = word.toLowerCase();
            String token;
            if (keywords.contains(lw) || operators.contains(word) || symbols.contains(word) || word.matches("\\d+(\\.\\d+)?")) {
                token = "< " + word + " >";
            } else {
                idMap.putIfAbsent(word, id++);
                token = "<id," + idMap.get(word) + ">";
            }
            System.out.println((word.length() < 8 ? word + "\t\t" : word + "\t") + token);
        }
    }
}
