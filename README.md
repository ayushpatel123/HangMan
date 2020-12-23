# HangMan
/* Name: Ayush Patel
 * Purpose: To create a a game like HangMan. This game has three options,
 * 			one word, phrases, and multiplayer. Near the end, you have an 
 * 			option to guess the entire word. You have to guess each letter 
 * 			until you have guessed each letter in the game. 
 */

import java.util.ArrayList;
import java.util.Random;
import java.util.Scanner;
public class HangMan {

	
	public static void main(String[] args) {
		
		Scanner input = new Scanner (System.in);
		Random rand = new Random();
		
		String answer, word = "", randWord = "", multiplayerWord = "";
		int  choice = 0;
	
		do
		{
			do
			{
				choice = 0;
				System.out.println("Welcome to Hangman");
				System.out.println("Try and guess the word before you die\n\n");
				System.out.println("Rules:");
				System.out.println("1. You must enter only a letter (NOT WORDS) unless prompted");
				System.out.println("2. Each time an incorrect letter is entered, you lose a life and gain a limb");
				System.out.println("3. When you have 2 lives left, you will get an option to pick the word");
				System.out.println("4. If you guess the entire word correctly, You Win!");
				System.out.println("5. In Multiplayer mode, you cannot enter phrases, only one word will be accecptable\n\n");
				System.out.println("Would you like to play the Easy mode, Hard mode or multiplayer(1, 2, 3)");
				choice = input.nextInt();
				
				if (choice == 1)
				{
					
					int word1 = 0;
					word1 = rand.nextInt(6) + 1;
					switch(word1)
					{
					case 1:
						randWord = "mango";
						break;
					case 2:
						randWord = "hello";
					case 3:
						randWord = "hangman";
						break;
					case 4:
						randWord = "jazz";
					case 5:
						randWord = "banjo";
					default:
						randWord = "java";
						break;
					} // End of switch statement
					word = randWord;
					break;
				}
					
				else if (choice == 2)
				{
					int word1 = 0;
					word1 = rand.nextInt(4) + 1;
					switch(word1)
					{
					case 1:
						randWord = "welcome to hangman";
						break;
					case 2:
						randWord = "our planet is earth";
					case 3:
						randWord = "my favorite color is blue";
						break;
					default:
						randWord = "my favorite sport is soccer";
						break;
					}
				
					word = randWord;
					break;
				}
				
				else if (choice == 3)
				{
					System.out.println("Enter a word for someone else to guess, a single word only, NO SPACES");
					multiplayerWord = input.next();
					word = multiplayerWord;
					break;
				}
				
				else 
				{
					System.out.println("Invalid Input");
				}
			
			} while ((choice != 1) || choice != 2 || choice != 3);
			
			System.out.print("                       ____\r\n" + 
					"                      |    |      \r\n" + 
					"                      |          \r\n" + 
					"                      |         \r\n" + 
					"       		      |    \r\n" + 
					"                      |   \n" + 
					"                     _|_\n" + 
					"                    |   |______\r\n" + 
					"                    |          |\r\n" + 
					"                    |__________|\n\n");
			System.out.println("\n\n");
			
			int life = 6;
			
			// Game Method
			guess(word,life);
			
			// Check to see validity of user input
			do
			{
				answer = "";
				System.out.println("Do you want to play again (Y or N)");
				answer = input.next();
				 
				if (answer.equalsIgnoreCase("N"))
				{
					System.out.println("You have exited this application");
					System.exit(0);
				}
				
			} while (!answer.equalsIgnoreCase("Y"));		
			
		} while (answer.equalsIgnoreCase("Y"));	
		
		
	} // End of main method
	
	
	public static void guess(String word, int life)
	{
		
		// Declare Variables
		String choice;
		
		Scanner input = new Scanner (System.in);
		
		
		char [] chosenWord = new char[word.length()];
		
		// Replace letter if it is correct
		for (int i = 0; i < word.length(); i++)
		{
			
			// Display letters as blanks for user to fill in, and replace if correct
			chosenWord [i] = '-';
			if (word.charAt(i) == ' ')
			{
				chosenWord[i] = ' ';
			}
		} // End of for loop
		
		
		// Print out what letters you have guessed so far
		System.out.print("Word: ");
		System.out.print(chosenWord);
		System.out.println("           Life Remaining " + life); 
		
		// Store all letters entered here to be displayed for user if entered again
		ArrayList  <Character> a = new ArrayList <Character>();
		
		// Play the game while lives are greater than 0
		while(life > 0)
		{
			// Input letter guessed
			System.out.print("Guess: ");
			char letter = input.next().charAt(0);
			
			
			
			// Check if letter is already entered and display used letters
			if (a.contains(letter))
			{
				System.out.println("Already entered");
				System.out.println("You have already used these letters: " + a);
				System.out.println("Enter another letter");
				continue;
			}
			
			// Add letter inside array list
			a.add(letter);
			
			// Check if letter is already entered
			if (word.contains(letter + ""))
			{
				for (int y = 0; y < word.length(); y++)
				{
					if (word.charAt(y) == letter)
					{
						chosenWord[y] = letter;
						
					}
				} // End of for loop
			} // End of first if 
			
			// If letter entered is incorrect, draw a new limb and subtract a life
			else 
			{
				
				life--;
				if (life == 5)
				{
					
					System.out.print("                       ____\r\n" + 
							"                      |    |      \r\n" + 
							" INCORRECT LETTER     |    o      \r\n" + 
							"    TRY AGAIN         |        \r\n" + 
							"       		      |    \r\n" + 
							"                      |   \n" + 
							"                     _|_\n" + 
							"                    |   |______\r\n" + 
							"                    |          |\r\n" + 
							"                    |__________|\n\n");
					System.out.println("\n\n");
				}
				
				else if (life ==4)
				{
					System.out.print("                       ____\r\n" + 
							"                      |    |      \r\n" + 
							" INCORRECT LETTER     |    o      \r\n" + 
							"    TRY AGAIN         |    |    \r\n" + 
							"       		      |    \r\n" + 
							"                      |   \n" + 
							"                     _|_\n" + 
							"                    |   |______\r\n" + 
							"                    |          |\r\n" + 
							"                    |__________|\n\n");
					System.out.println("\n\n");
				
				}
				
				else if (life == 3)
				{
					System.out.print("                       ____\r\n" + 
							"                      |    |      \r\n" + 
							" INCORRECT LETTER     |    o      \r\n" + 
							"    TRY AGAIN         |    |\\    \r\n" + 
							"       		      |         \n" + 
							"                       |   \n" + 
							"                     _|_\n" + 
							"                    |   |______\r\n" + 
							"                    |          |\r\n" + 
							"                    |__________|\n\n");
					System.out.println("\n\n");
				}
				
				else if (life == 2)
				{
					System.out.print("                       ____\r\n" + 
							"                      |    |      \r\n" + 
							" INCORRECT LETTER     |    o      \r\n" + 
							"    TRY AGAIN         |   /|\\  \r\n" + 
							"       		      |             \r\n" + 
							"                     |   \n" + 
							"                     _|_\n" + 
							"                    |   |______\r\n" + 
							"                    |          |\r\n" + 
							"                    |__________|\n\n");
					System.out.println("\n\n");
					
					// Allow user to guess the entire word
					if (life == 2)
					{
						String answer1 = "";
						System.out.println("Do you want to guess the word? No lives will be taken off (Y or N)");
						String wordGuess = "";
						answer1 = input.next();
						
						if (answer1.equalsIgnoreCase("Y"))
						{
							System.out.println("Enter word\n");
							wordGuess = input.next();
							if (wordGuess.equals(word))
							{
								System.out.println("You guessed correctly");
								System.out.println(word);
								break;
							}
							else 
							{
								System.out.println("You Guessed incorrectly. Keep on going \n");
								System.out.print(chosenWord);
								continue;
							}
						}
					} 
				}
				
				else if (life == 1)
				{
					System.out.print("                       ____\r\n" + 
							"                      |    |      \r\n" + 
							" INCORRECT LETTER     |    o      \r\n" + 
							"    TRY AGAIN         |   /|\\ \r\n" + 
							"       		      |     \\" + 
							"                      |   \n" + 
							"                     _|_\n" + 
							"                    |   |______\r\n" + 
							"                    |          |\r\n" + 
							"                    |__________|\n\n");
					System.out.println("\n\n");
				}
			}
			
			// winning and losing conditions
			if (word.equals(String.valueOf(chosenWord)))
			{
				System.out.println("You were right, the word was " + word + "!");
				System.out.println("Congratulations, You Won");
				break;
			}
			
			System.out.print(chosenWord);
			System.out.println("   Life Remaining: " + life);
			
		} // End of while statement
		
			if (life ==0)
			{
				System.out.println("You Lose");
				System.out.print("                       ____\r\n" + 
						"                      |    |      \r\n" + 
						"    GAMEOVER          |    o      \r\n" + 
						"                      |   /|\\ \r\n" + 
						"       		      |   / \\\n" + 
						"                      |   \n" + 
						"                     _|_\n" + 
						"                    |   |______\r\n" + 
						"                    |          |\r\n" + 
						"                    |__________|\n\n");
				System.out.println("\n\n");
			}
		
	} // End of guess method
	
} // End of program




