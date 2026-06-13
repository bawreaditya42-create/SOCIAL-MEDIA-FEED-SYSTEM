import java.util.ArrayList;
import java.util.Date;
import java.util.List;

class Post {
    private String username;
    private String content;
    private Date timestamp;

    public Post(String username, String content) {
        this.username = username;
        this.content = content;
        this.timestamp = new Date();
    }

    public void displayPost() {
        System.out.println("----------------------------");
        System.out.println("User: " + username);
        System.out.println("Post: " + content);
        System.out.println("Time: " + timestamp);
    }
}

class SocialMediaFeed {
    private List<Post> posts;

    public SocialMediaFeed() {
        posts = new ArrayList<>();
    }

    public void addPost(String username, String content) {
        posts.add(new Post(username, content));
        System.out.println("Post added successfully!");
    }

    public void displayFeed() {
        if (posts.isEmpty()) {
            System.out.println("No posts available.");
            return;
        }

        System.out.println("\n===== SOCIAL MEDIA FEED =====");
        for (int i = posts.size() - 1; i >= 0; i--) {
            posts.get(i).displayPost();
        }
    }
}

public class Main {
    public static void main(String[] args) {
        SocialMediaFeed feed = new SocialMediaFeed();

        feed.addPost("Aditya", "Hello everyone!");
        feed.addPost("Rahul", "Learning Java OOP today.");
        feed.addPost("Priya", "Good morning friends!");

        feed.displayFeed();
    }
}
