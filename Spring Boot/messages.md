Completable feature
```java
import java.net.URI;
import java.util.concurrent.CompletableFuture;

public class AsyncService {

    // Simulated method to send a message asynchronously
    public CompletableFuture<String> sendMessageAsync(URI uri, String message) {
        CompletableFuture<String> future = new CompletableFuture<>();

        // Simulate an asynchronous operation
        new Thread(() -> {
            try {
                // Simulate sending the message to the given URI
                // For example, you could make an HTTP request here

                // For demo purposes, we just simulate a delay
                Thread.sleep(1000); // Simulate network delay

                // Simulate a response
                String response = "Message sent to " + uri.toString() + " with content: " + message;

                // Complete the future with the response
                future.complete(response);
            } catch (InterruptedException e) {
                future.completeExceptionally(e);
            }
        }).start();

        return future;
    }
}

```