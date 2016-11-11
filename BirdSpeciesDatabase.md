# First
/**@author Joya
 * I referred to the file ColorsArrayList from the study materials to guide me through this activity
 */

package assessment;
import javax.swing.JOptionPane;
import java.util.*;
public class BirdArrayList {
//I used the following method to create a new array containing bird species
	public static void main(String[] args) {
		ArrayList<String>BirdSpecies=new ArrayList<String>();
		BirdSpecies.add("Mackaw");
		BirdSpecies.add("Blue Jay");
		BirdSpecies.add("Lovebird");
		BirdSpecies.add("Flamingo");
		BirdSpecies.add("Peacock");
		
		char response;
		
			/**The following code uses a do while loop to create a menu for the user. Their response will dictate what happens next.
			 * The "E" option allows the user to exit the program
			 * the do while loop and program will continue to run as long as "E" is not entered.
			 * If "E" is entered, the program will end
			 * @param birdSpecies Bird Species List
			 */
		do
		{
			String answer=JOptionPane.showInputDialog("Enter '+' to add a bird species \n" 
					+ "Enter '-' to remove a bird species \n" + "Enter 'S' to search for a bird species \n"
					+ "Enter 'D' to display the entire bird species list \n" + "Enter 'E' to exit the program");
					
			response=answer.charAt(0);
			
			if (response =='+') addToArray(BirdSpecies);
			else
				if (response == '-' )removeFromArray(BirdSpecies);
				else
					if (response =='S')searchArray(BirdSpecies);
					else
						if (response =='D')displayArray(BirdSpecies);
			
		}
		while(response !='E');

	}
	/**the following code executes if  'D' is selected by user
	 *@param birdSpecies Bird Species List
	 */
	private static void displayArray(ArrayList<String> birdSpecies) {
		int i;
		for(i=0;i<birdSpecies.size();i++)
			System.out.println(birdSpecies.get(i));
		
	}
	/**the following code executes if  'S' is selected by user. 
	*It uses a binary search to find the bird species that was entered by user
	*@param birdSpecies Bird Species List
	*/

	private static void searchArray(ArrayList<String> birdSpecies) {
		int low,med,high;
		int returnValue=-1;
		boolean found=false;
		String searchValue=JOptionPane.showInputDialog(null, "Enter bird species to search for ");
		
		Collections.sort(birdSpecies);
		low=0;
		high=birdSpecies.size();
		
		while(!found)
		{
			med=(high+low)/2;
			if (searchValue.compareTo(birdSpecies.get(med))==0)
			{
			returnValue=med;
			found=true;
			}
			else
				if(low-high<2)
				{
					returnValue=-1;
					found=true;
				}
				else
					if(searchValue.compareTo(birdSpecies.get(med))>0)
					low=med;
					else
						high=med;
			if (returnValue==-1)
				JOptionPane.showMessageDialog(null, "Bird species not found");
			else
				JOptionPane.showMessageDialog(null, "Bird species found at Index" + returnValue + ".");
			
		}
	}
	/** the following code uses a sequencial search to find the entered bird species to be removed
	 * @param birdSpecies Bird Species List
	 */

	private static void removeFromArray(ArrayList<String> birdSpecies) {
		int i;
		boolean found = false;
		String answer=JOptionPane.showInputDialog(" Enter the bird species to be removed from the list");
		
		for (i=0;i<birdSpecies.size();i++)
			if(answer.equals(birdSpecies.get(i)))
			{
				found=true;
				birdSpecies.remove(i);
				displayArray(birdSpecies);
			}
			if(found==false)
				JOptionPane.showMessageDialog(null, "The Species that you've entered was not found");
		
	}
	/**
	 * the following code executes if  'A' is selected by user
	 * @param birdSpecies Bird Species List
	 */
	private static void addToArray(ArrayList<String> birdSpecies) {
		String answer=JOptionPane.showInputDialog(" Enter the bird species to be added to the list");
		birdSpecies.add(birdSpecies.size(), answer);
		displayArray(birdSpecies);
		
	}

}
