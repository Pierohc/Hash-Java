    import java.security.MessageDigest;
    import java.security.NoSuchAlgorithmException;
    import java.nio.charset.StandardCharsets;
    
    public class HashingExample {
    
        public static String hashString(String input) {
            try {
                // Obtener una instancia de MessageDigest con el algoritmo SHA-256
                MessageDigest digest = MessageDigest.getInstance("SHA-256");
    
                // Convertir el string a bytes y hashear
                byte[] encodedHash = digest.digest(
                        input.getBytes(StandardCharsets.UTF_8));
    
                // Convertir el hash en representación hexadecimal
                StringBuilder hexString = new StringBuilder();
                for (byte b : encodedHash) {
                    String hex = Integer.toHexString(0xff & b);
                    if (hex.length() == 1) {
                        hexString.append('0');
                    }
                    hexString.append(hex);
                }
    
                return hexString.toString();
            } catch (NoSuchAlgorithmException e) {
                // Manejar la excepción en caso de que el algoritmo no esté disponible
                e.printStackTrace();
                return null;
            }
        }
    
        public static void main(String[] args) {
            String inputString = "Hola, mundo!";
            String hashedString = hashString(inputString);
    
            System.out.println("Input String: " + inputString);
            System.out.println("Hashed String: " + hashedString);
        }
    }
