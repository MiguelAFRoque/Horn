import java.util.ArrayList;
import java.util.Arrays;
import java.util.Scanner;
import java.util.HashSet;
import java.util.Set;
/**
 *
 * @author Miguel Roque a39466 PL2
 *         André Pires a44415 PL4
 */

public class Final {
    
   public static String rmvDup(String str) {        //remove duplicated chars oon a string
        Set<Character> chars = new HashSet<>();
        StringBuilder output = new StringBuilder(str.length());

        for (int i = 0; i < str.length(); i++) {
            char ch = str.charAt(i);
            if (chars.add(ch)) {
                output.append(ch);
            }
        }

        return output.toString();
    }
   
   public static boolean compareStrings(String str, String cf){         //compare two strings
        boolean res = true;                                                 //variable res starts true (V)
        for (int i = 0; i < str.length(); i++) {
            for (int j = 0; j < cf.length(); j++) {
                if(cf.indexOf(str.charAt(i)) != -1 ){                    //if char is in string:
                    res = res && true;                                      // variable res = V & V = V
                }else res = res && false;                                   // else: V & F = F
                
            }
            
        }
        return res;
    }
    
    public static void main(String[] args) {
        int npos = 0;   //número de positivos na cláusula
        
        //(~p | a ) & (p) & (~p | ~R | x) & (~W | P | ~h) & (F) & (~f |~q | e) & (~t | ~k | ~l)
        //UNSAT (~p | R ) & (~x) & (p) & (~p | x | ~R | x)
        //(~p | Q | ~r) & (~t) & (P) & (~T | x | Z) & (F)
        
        Scanner obj = new Scanner(System.in);  //Create scanner to read input
        String str = obj.nextLine();        //copy input to sting
        
        str = str.replaceAll("\\s","");
        
        //create new clausula
        String[] clau = str.split("&");
        
        String conjfinal = "/";    //String with final set (where / is top)
        
        String[] imp = new String[clau.length];
        
            for (int i = 0; i < clau.length; i++) {     //going through every clause 

                String strpos = "";                     //String with letters  
                String strneg = "";                     //String with negative letters
                for(int k = 0; k <clau[i].length(); k++){   //clausula i positions
                       
                    if(Character.isLetter(clau[i].charAt(k)) == true && clau[i].charAt(k-1) != '~'){   //is it a letter and is it not negative?
                        strpos = strpos + clau[i].charAt(k);
                    }
                    if (Character.isLetter(clau[i].charAt(k)) == true && clau[i].charAt(k-1) == '~') {  //is it negative?
                        strneg = strneg + clau[i].charAt(k);
                    }
                }
                
                String novo = rmvDup(strpos);      //Unrepeated positive chars
                String novo1 = rmvDup(strneg);      //Unrepeated negative chars
                
                if(novo.equals("")){
                    novo = novo + "!";          //! is the value of botom
                }
                
                if (novo1.equals("")) {
                    novo1 = novo1 + "/";        //  / is top
                }
                
                
                //negative _ positive where _ means -> (implica)
                
                imp[i] = novo1 + "_" + novo;
                    if (novo1.equals("/")) {
                        conjfinal = conjfinal + novo;
                    }
                    //System.out.println("conjunto Final = " + conjfinal);
                               
                if (novo.length() >= 2) {
                    System.out.println("NA");       //---------Not Horn form
                    return;
                }               
                
                
            }
            
            String[] left = new String[clau.length];
            String[] right = new String[clau.length];
            
            for (int i = 0; i < clau.length; i++) {
                String clause = imp[i];
                //System.out.println("Clausula:");
                //System.out.println(clause);
                String[] sides = clause.split("_");
                
                left[i] = rmvDup(sides[0]); 
                right[i] = sides[1];            // on the right side of the formula, here can only be one char
                /*System.out.println("left:");
                System.out.println(left[i]);
                System.out.println("right:");
                System.out.println(right[i]);
                System.out.println("--------------------");*/
            
            }
            /*System.out.println("All Lefts:");
            for (int i = 0; i < left.length; i++) {
                
                System.out.println(left[i]);
            
            }*/
            
            
            for (int i = 0; i < clau.length; i++) {
                int nleft = left.length;
                for (int j = 0; j < nleft; j++) {
                    //System.out.println("Nleft="+nleft);
                    conjfinal = rmvDup(conjfinal);              //shorten final set 
                    if (compareStrings(left[j], conjfinal)) {
                        conjfinal = conjfinal + right[j];
                    }
                }
            }
            
            conjfinal = rmvDup(conjfinal);
            //System.out.println("Conjunto FINAL = "+conjfinal);
            
            if (compareStrings("!",conjfinal)) {
                System.out.println("UNSAT");
                return;
        }
            
            System.out.println("SAT");              //-------- Horn form
            
            
    }
    
}
