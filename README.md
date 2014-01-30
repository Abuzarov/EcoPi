EcoPi
=====

Raspberry Pi to auto detect temperature and predict weather pattern for central heating system.


	import java.io.*;
	import java.net.*;
import javax.swing.*;
    
	
	public class weather1 {
		
		public static String temp;
        public static String Heating;
		public static String postcode=JOptionPane.showInputDialog(null, "Enter first 4 characters in ur postcode : ", "EG: sg13", 1);
		
	               public static void main(String[] args) throws IOException {
	            	   try {
                           while (true) {
                           Gettemp();
                           txt();
                           txt2();
                           Heating =Weather3.comparing();
                           System.out.println(Heating);
                           Thread.sleep(3600000);
                        
                    }
                    }  catch (InterruptedException e) {
                       e.printStackTrace();
                  }
                  }

                   public static void txt() throws IOException, UnsupportedEncodingException{
                	   
                	        PrintWriter out = new PrintWriter(new BufferedWriter(new FileWriter("C:\\Users\\Askar_000\\Desktop\\Weather\\weather.txt", true)));
                		    out.print(temp + ";" + " ");
                		    out.close(); }
                   
                   public static void txt2()throws IOException, UnsupportedEncodingException{
                	        PrintWriter writer = new PrintWriter("C:\\Users\\Askar_000\\Desktop\\Weather\\Current_weather.txt", "UTF-8");
                	        writer.println(temp);
                	        writer.close(); }
                   
                   public static void Gettemp(){
	            	   URL url;
	                   InputStream is = null;
	                   BufferedReader br;
	                   String line;
	                   
	                  
	                   String line2="";
	                   
	                  
	                   try {
	                       url = new URL("http://www.bbc.co.uk/weather/"+postcode);
	                       is = url.openStream(); 
	                       br = new BufferedReader(new InputStreamReader(is));
	                       while ((line = br.readLine()) != null) {
	                                             line2=line2+line+"\n";
	                                             if(line.contains("<span data-unit=\"c\" class=\"units-value temperature-value")){
	                                                            line2=line;
	                                                            break;
	                                             }
	                                        
	                                             }
	                                                 temp = ""+line.charAt(143);
	                                                 if((char)line.charAt(144)<58 && (char)line.charAt(144)>47){
	                                                	 
	                                                            temp = temp+line2.charAt(144);
	                                                 }
	                                                 if((char)line.charAt(145)<58 && (char)line.charAt(145)>47){
	                                                          
	                                                            temp = temp+line2.charAt(145);
	                                                 }          
	                                                 
	                                  System.out.println(temp);
	                                  
	                          
	           	                   
	                   } catch (MalformedURLException mue) {
	                        mue.printStackTrace();
	                   } catch (IOException ioe) {
	                        ioe.printStackTrace();
	                   } finally {
	                       try {
	                           if (is != null) is.close();
	                       } catch (IOException ioe) {
	                     
	                       }
	                   }
	                   }
	              
	               }
