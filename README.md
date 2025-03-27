import java.io.*;
import java.nio.file.*;
import java.security.*;
import com.google.gson.*;
public class MD5JsonParser {
    public static void main(String[] args) {
        try {
          
            String jsonContent = new String(Files.readAllBytes(Paths.get("input.json")));
            JsonObject jsonObject = JsonParser.parseString(jsonContent).getAsJsonObject();
           
            String firstName = jsonObject.get("first_name").getAsString().toLowerCase().replace(" ", "");
            String rollNumber = jsonObject.get("roll_number").getAsString().toLowerCase().replace(" ", "");

            String concatenatedString = firstName + rollNumber;
            
            String md5Hash = getMD5Hash(concatenatedString);

            Files.write(Paths.get("output.txt"), md5Hash.getBytes());
            System.out.println("MD5 hash written to output.txt: " + md5Hash);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
private static String getMD5Hash(String input) throws NoSuchAlgorithmException {
    MessageDigest md = MessageDigest.getInstance ("MD5");
    byte[] digest = md.digest();
    StringBuilder sb = new StringBuilder();
    for (byte b : digest) {
        sb.append(String.format("%02x", b));
    }
    return sb.toString();
}
}
