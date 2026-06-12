import java.util.*;

class Post {
    int postId;
    int userId;
    String content;
    long timestamp;

    public Post(int postId, int userId, String content) {
        this.postId = postId;
        this.userId = userId;
        this.content = content;
        this.timestamp = System.currentTimeMillis();
    }
}

class User {
    int userId;
    String name;
    Set<Integer> following = new HashSet<>();

    public User(int userId, String name) {
        this.userId = userId;
        this.name = name;
    }

    public void follow(int userId) {
        following.add(userId);
    }
}

class SocialMediaFeedSystem {
    Map<Integer, User> users = new HashMap<>();
    List<Post> posts = new ArrayList<>();

    // Create User
    public void addUser(int id, String name) {
        users.put(id, new User(id, name));
    }

    // Follow User
    public void followUser(int followerId, int followeeId) {
        if (users.containsKey(followerId)) {
            users.get(followerId).follow(followeeId);
        }
    }

    // Create Post
    public void createPost(int userId, int postId, String content) {
        posts.add(new Post(postId, userId, content));
    }

    // Get Feed
    public List<Post> getFeed(int userId) {
        List<Post> feed = new ArrayList<>();

        User user = users.get(userId);

        for (Post post : posts) {
            if (post.userId == userId ||
                user.following.contains(post.userId)) {
                feed.add(post);
            }
        }

        feed.sort((a, b) -> Long.compare(b.timestamp, a.timestamp));
        return feed;
    }

    public static void main(String[] args) {
        SocialMediaFeedSystem system = new SocialMediaFeedSystem();

        system.addUser(1, "Aditya");
        system.addUser(2, "Rahul");
        system.addUser(3, "Priya");

        system.followUser(1, 2);
        system.followUser(1, 3);

        system.createPost(2, 101, "Hello from Rahul!");
        system.createPost(3, 102, "Good Morning!");
        system.createPost(1, 103, "My First Post");

        List<Post> feed = system.getFeed(1);

        System.out.println("Feed for Aditya:");
        for (Post p : feed) {
            System.out.println(
                "PostID: " + p.postId +
                " UserID: " + p.userId +
                " Content: " + p.content
            );
        }
    }
}
