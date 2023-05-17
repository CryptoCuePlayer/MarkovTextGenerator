# MarkovTextGenerator
MarkovTextGenerator
import java.util.HashMap;
import java.util.Map;
import java.util.Random;

public class MarkovTextGenerator {
    private Map<String, String[]> markovChain;
    private String currentPrefix;

    public MarkovTextGenerator() {
        this.markovChain = new HashMap<>();
        this.currentPrefix = "";
    }

    public void train(String text) {
        String[] words = text.split("\\s+");
        for (String word : words) {
            String[] suffixes = markovChain.getOrDefault(currentPrefix, new String[0]);
            String[] updatedSuffixes = new String[suffixes.length + 1];
            System.arraycopy(suffixes, 0, updatedSuffixes, 0, suffixes.length);
            updatedSuffixes[suffixes.length] = word;
            markovChain.put(currentPrefix, updatedSuffixes);
            currentPrefix = word;
        }
    }

    public String generateText(int length) {
        StringBuilder text = new StringBuilder();
        String prefix = "";
        Random random = new Random();
        for (int i = 0; i < length; i++) {
            String[] suffixes = markovChain.getOrDefault(prefix, new String[0]);
            if (suffixes.length == 0) {
                prefix = "";
            } else {
                String nextWord = suffixes[random.nextInt(suffixes.length)];
                text.append(nextWord).append(" ");
                prefix = nextWord;
            }
        }
        return text.toString().trim();
    }

    public static void main(String[] args) {
        MarkovTextGenerator generator = new MarkovTextGenerator();
        generator.train("Lorem ipsum dolor sit amet consectetur adipiscing elit");
        generator.train("sed do eiusmod tempor incididunt ut labore et dolore magna aliqua");
        String generatedText = generator.generateText(10);
        System.out.println(generatedText);
    }
}
