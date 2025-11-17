import javafx.application.Application;
import javafx.geometry.Insets;
import javafx.scene.Scene;
import javafx.scene.control.*;
import javafx.scene.layout.*;
import javafx.stage.Stage;
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;
import javax.crypto.spec.GCMParameterSpec;
import java.nio.charset.StandardCharsets;
import java.security.SecureRandom;
import java.util.Base64;
import java.util.LinkedHashMap;
import java.util.Map;
public class PasswordManager extends Application {
    private static final String AES_TRANSFORM = "AES/GCM/NoPadding";
    private static final int GCM_TAG_BITS = 128;        // 16 bytes tag
    private static final int IV_BYTES = 12;             // 12 bytes recommended for GCM
    private static final int AES_KEY_BITS = 128;
    private TextField websiteField;
    private TextField usernameField;
    private PasswordField passwordField;
    private TextArea outputArea;
    private SecretKey secretKey;
    // LinkedHashMap keeps insertion order when viewing
    private final Map<String, String> passwordStorage = new LinkedHashMap<>();
    private final SecureRandom secureRandom = new SecureRandom();
    @Override
    public void start(Stage stage) {
        // AES Key Generation
        try {
            KeyGenerator keyGen = KeyGenerator.getInstance("AES");
            keyGen.init(AES_KEY_BITS);
            secretKey = keyGen.generateKey();
        } catch (Exception e) {
            // If key creation fails, disable functionality early.
            showError("Failed to initialize encryption key: " + e.getMessage());
            return;
        }
        // UI Elements
        Label websiteLabel = new Label("Website:");
        websiteField = new TextField();
        Label usernameLabel = new Label("Username:");
        usernameField = new TextField();
        Label passwordLabel = new Label("Password:");
        passwordField = new PasswordField();
        Button saveBtn = new Button("Save Password");
        Button viewBtn = new Button("View All");
        Button generateBtn = new Button("Generate Password");
        outputArea = new TextArea();
        outputArea.setEditable(false);
        outputArea.setWrapText(true);
        // Button Actions
        saveBtn.setOnAction(e -> savePassword());
        viewBtn.setOnAction(e -> viewPasswords());
        generateBtn.setOnAction(e -> passwordField.setText(generatePassword(12)));
        // Layout
        VBox layout = new VBox(10);
        layout.setPadding(new Insets(15));
        layout.getChildren().addAll(
                websiteLabel, websiteField,
                usernameLabel, usernameField,
                passwordLabel, passwordField,
                new HBox(10, saveBtn, viewBtn, generateBtn),
                new Label("Stored Passwords:"),
                outputArea
        );
        // Scene Setup
        Scene scene = new Scene(layout, 420, 520);
        stage.setTitle("Password Manager (AES-GCM Encrypted)");
        stage.setScene(scene);
        stage.show();
    }
    private void savePassword() {
        String website = websiteField.getText().trim();
        String username = usernameField.getText().trim();
        String password = passwordField.getText().trim();

        if (website.isEmpty() || username.isEmpty() || password.isEmpty()) {
            outputArea.setText("⚠️ Please fill all fields.");
            return;
        }
        try {
            String encryptedPassword = encrypt(password);
            passwordStorage.put(website + " (" + username + ")", encryptedPassword);
            outputArea.setText("✅ Password saved for " + website);
            websiteField.clear();
            usernameField.clear();
            passwordField.clear();
        } catch (Exception e) {
            outputArea.setText("❌ Error encrypting password: " + e.getMessage());
        }
    }
    private void viewPasswords() {
        if (passwordStorage.isEmpty()) {
            outputArea.setText("No passwords saved yet.");
            return;
        }
        StringBuilder sb = new StringBuilder("🔐 Saved Passwords:\n\n");
        for (Map.Entry<String, String> entry : passwordStorage.entrySet()) {
            try {
                String decrypted = decrypt(entry.getValue());
                sb.append(entry.getKey()).append(" → ").append(decrypted).append("\n");
            } catch (Exception e) {
                sb.append(entry.getKey()).append(" → [Error decrypting]\n");
            }
        }
        outputArea.setText(sb.toString());
    }
    private String generatePassword(int length) {
        // Excludes ambiguous characters if you want: O/0, I/l, etc. (optional)
        final String chars = "ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnopqrstuvwxyz123456789!@#$%^&*";
        StringBuilder sb = new StringBuilder(length);
        for (int i = 0; i < length; i++) {
            int idx = secureRandom.nextInt(chars.length());
            sb.append(chars.charAt(idx));
        }
        return sb.toString();
    }
    /**
     * Encrypts using AES-GCM. The returned string is Base64( IV || CIPHERTEXT || TAG ).
     */
    private String encrypt(String plainText) throws Exception {
        byte[] iv = new byte[IV_BYTES];
        secureRandom.nextBytes(iv);
        Cipher cipher = Cipher.getInstance(AES_TRANSFORM);
        GCMParameterSpec spec = new GCMParameterSpec(GCM_TAG_BITS, iv);
        cipher.init(Cipher.ENCRYPT_MODE, secretKey, spec);
        byte[] ciphertext = cipher.doFinal(plainText.getBytes(StandardCharsets.UTF_8));
        // Concatenate IV + ciphertext+tag (tag is appended by GCM at the end of ciphertext)
        byte[] out = new byte[iv.length + ciphertext.length];
        System.arraycopy(iv, 0, out, 0, iv.length);
        System.arraycopy(ciphertext, 0, out, iv.length, ciphertext.length);
        return Base64.getEncoder().encodeToString(out);
        }
    /**
     * Decrypts Base64( IV || CIPHERTEXT || TAG ).
     */
    private String decrypt(String encoded) throws Exception {
        byte[] input = Base64.getDecoder().decode(encoded);
        if (input.length < IV_BYTES + 1) {
            throw new IllegalArgumentException("Ciphertext too short");
        }
        byte[] iv = new byte[IV_BYTES];
        byte[] ciphertext = new byte[input.length - IV_BYTES];
        System.arraycopy(input, 0, iv, 0, IV_BYTES);
        System.arraycopy(input, IV_BYTES, ciphertext, 0, ciphertext.length);
        Cipher cipher = Cipher.getInstance(AES_TRANSFORM);
        GCMParameterSpec spec = new GCMParameterSpec(GCM_TAG_BITS, iv);
        cipher.init(Cipher.DECRYPT_MODE, secretKey, spec);
        byte[] plain = cipher.doFinal(ciphertext);
        return new String(plain, StandardCharsets.UTF_8);
    }
    private void showError(String msg) {
        // Minimal fallback UI if key gen fails
        Alert alert = new Alert(Alert.AlertType.ERROR, msg, ButtonType.CLOSE);
        alert.setHeaderText("Initialization Error");
        alert.showAndWait();
    }
    public static void main(String[] args) {
        launch(args);
    }
}
