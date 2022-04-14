import java.io.FileOutputStream;
import java.io.IOException;
import java.net.HttpURLConnection;
import java.net.URL;
import java.nio.channels.Channels;
import java.nio.channels.ReadableByteChannel;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;
import java.util.List;

public class BlogPostDownloader {

    // Example for downloading blog posts
    public static void main(String[] args) throws Exception  {
        String url = "https://www.engadget.com/2019-08-25-sony-and-yamaha-sc-1-sociable-cart.html";
        System.out.println(download(url));
    }

    public static List<String> download(String url) throws IOException {
        URL website = new URL(url);
        HttpURLConnection connection = (HttpURLConnection) website.openConnection();
        connection.setRequestProperty("User-Agent", "custom agent");
        ReadableByteChannel rbc = Channels.newChannel(connection.getInputStream());

        Path tmpFile = Files.createTempFile("temp_exercise", ".txt");
        List<String> result = null;
        try {
            FileOutputStream fos = new FileOutputStream(tmpFile.toFile());
            fos.getChannel().transferFrom(rbc, 0, Long.MAX_VALUE);
            result = new ArrayList<>(Files.readAllLines(tmpFile));
        } finally {
            Files.deleteIfExists(tmpFile);
        }
        return result;
    }
}
