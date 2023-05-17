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
