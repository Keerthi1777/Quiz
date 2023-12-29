import java.util.Scanner;

public class QuizApp {
    public static void main(String[] args) {
        // Create questions
        Question q1 = new Question("What is the capital of France?", new String[]{"Berlin", "Paris", "Madrid"}, 1);
        Question q2 = new Question("Which programming language is this quiz written in?", new String[]{"Java", "Python", "C++"}, 0);

        // Create a quiz
        Quiz myQuiz = new Quiz();
        myQuiz.addQuestion(q1);
        myQuiz.addQuestion(q2);

        // Initialize Scanner for user input
        Scanner scanner = new Scanner(System.in);

        // Quiz interaction
        int score = 0;

        for (int i = 0; i < myQuiz.getQuizSize(); i++) {
            Question currentQuestion = myQuiz.getQuestion(i);

            // Display the question
            System.out.println("Question " + (i + 1) + ": " + currentQuestion.getQuestionText());

            // Display options
            String[] options = currentQuestion.getOptions();
            for (int j = 0; j < options.length; j++) {
                System.out.println((j + 1) + ". " + options[j]);
            }

            // Get user input
            int userChoice = -1;
            boolean validInput = false;

            while (!validInput) {
                System.out.print("Your answer (1-" + options.length + "): ");
                if (scanner.hasNextInt()) {
                    userChoice = scanner.nextInt();
                    if (userChoice >= 1 && userChoice <= options.length) {
                        validInput = true;
                    } else {
                        System.out.println("Invalid input. Please enter a number between 1 and " + options.length + ".");
                    }
                } else {
                    System.out.println("Invalid input. Please enter a number.");
                    scanner.next(); // consume the invalid input
                }
            }

            // Check user response
            if (userChoice - 1 == currentQuestion.getCorrectAnswerIndex()) {
                System.out.println("Correct!\n");
                score++;
            } else {
                System.out.println("Incorrect. The correct answer is: " + options[currentQuestion.getCorrectAnswerIndex()] + "\n");
            }
        }

        // Display final score
        System.out.println("Quiz completed. Your score: " + score + "/" + myQuiz.getQuizSize());

        // Close the scanner
        scanner.close();
    }
}
