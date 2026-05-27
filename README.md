# RockPaperScissors

import javafx.application.Application;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.VBox;
import javafx.stage.Stage;
import java.util.Random;

//annika wrote this!
public class RPS extends Application {

    Label result = new Label("   Choose Rock, Paper, or Scissors");

    Random rand = new Random();

    int playerScore = 0;
    int computerScore = 0;
    int rounds;
    int currentRound = 1;

    public void start(Stage stage) {

        TextInputDialog dialog = new TextInputDialog();
        dialog.setHeaderText("Best out of how many rounds?");
        dialog.setContentText("Enter odd number:");

        rounds = Integer.parseInt(dialog.showAndWait().get());

        Label title = new Label("   Rock Paper Scissors");
        title.setStyle("-fx-text-fill: black; -fx-font-size: 25;");

        Button rock = new Button("Rock");
        Button paper = new Button("Paper");
        Button scissors = new Button("Scissors");

        //we used AI to make our game pink 
        //we asked how to make everything pink
        rock.setStyle("-fx-background-color: pink;");
        paper.setStyle("-fx-background-color: pink;");
        scissors.setStyle("-fx-background-color: pink;");

        rock.setOnAction(e -> play("Rock"));
        paper.setOnAction(e -> play("Paper"));
        scissors.setOnAction(e -> play("Scissors"));

        result.setStyle("-fx-text-fill: darkpink;");

        VBox layout = new VBox(15);

        layout.getChildren().addAll(title,result,rock,paper,scissors);

        layout.setStyle("-fx-background-color: lightpink;");
        layout.setSpacing(15);

        Scene scene = new Scene(layout,300,300);

        stage.setScene(scene);
        stage.setTitle("Pink RPS");
        stage.show();
    }
    //shanvi did this!
    public void play(String userChoice) {

        int needed = rounds / 2 + 1;

        if(playerScore >= needed || computerScore >= needed)
            return;

        String[] choices = {"Rock","Paper","Scissors"};

        String computer = choices[rand.nextInt(3)];

        String outcome;

        if(userChoice.equals(computer))
            outcome = "   Tie!";

        else if(
                (userChoice.equals("Rock") && computer.equals("Scissors"))
                        ||
                (userChoice.equals("Paper") && computer.equals("Rock"))
                        ||
                (userChoice.equals("Scissors") && computer.equals("Paper"))
        ){

            outcome = "   You win!";
            playerScore++;
        }

        else{

            outcome = "   Computer wins!";
            computerScore++;
        }

        result.setText(
                "   Round: " + currentRound + "\n   You: " + userChoice +"\n   Computer: " + computer +"\n" + outcome +"\n\n   Score: You "+ playerScore +" - "+ computerScore+ " Computer"
        );
        currentRound++;

        if(playerScore >= needed ||
                computerScore >= needed){
            Alert end =
                    new Alert(
                            Alert.AlertType.INFORMATION
                    );

            if(playerScore >
                    computerScore)

                end.setHeaderText(
                        "You won the match!"
                );

            else
                end.setHeaderText("Computer won the match");
            end.setContentText(
                    "Final Score:\nYou: "+ playerScore +"\nComputer: "+ computerScore);
            end.show();
        }
    }
    public static void main(String[] args){
        launch(args);
    }
}
